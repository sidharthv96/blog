---
title: "Shrinking Mermaid"
date: 2022-11-20T12:19:15+05:30
toc: false
images:
tags:
  - mermaid
  - dependency
  - optimization
  - rollup
  - vite
---

# Mermaid

Mermaid is a markdown based diagramming tool. It is a javascript library that can be used to generate diagrams from text in a similar manner as markdown.

I've been a maintainer of the mermaid project for a while now. Mostly focused on the live editor, [mermaid.live](https://mermaid.live). 

Let's see how far we can shrink mermaid from it's current 2.05 MiB size.

# Types of bundles in Mermaid

## Standalone bundle - `mermaid.js`

This is usually imported directly by static sites via a `script` tag, and contains all dependencies required to render mermaid diagrams inside it. This is the largest bundle, with 0 external dependencies.

`mermaid.esm.mjs` is the ESM version of mermaid, which is the recommended version to use in modern browsers.

`mermaid.min.js` and `mermaid.esm.min.mjs` are minified versions of these bundles.

## Mermaid Core bundle - `mermaid.core.mjs`

This only contains the core mermaid code and is supposed to be used with bundlers like Vite/Webpack/etc when you are including mermaid as a dependency in your project. There is no minified build as it is expected that the bundler will minify the code.

## Package sizes

| Bundle              | Size        | gzip Size  |
| ------------------- | ----------- | ---------- |
| mermaid.core.mjs    | 1080.73 KiB | 217.63 KiB |
| mermaid.esm.mjs     | 2165.83 KiB | 455.45 KiB |
| mermaid.esm.min.mjs | 1554.08 KiB | 392.58 KiB |
| mermaid.js          | 2281.14 KiB | 460.57 KiB |
| mermaid.min.js      | 1148.52 KiB | 347.79 KiB |

# Composition of bundles

Just knowing that there are 3 bundles is not enough. We need to know what each bundle contains and how they are composed. Only then can we figure out how we can reduce the bundle size.

A quick google search landed me on [rollup-plugin-visualizer](https://github.com/btd/rollup-plugin-visualizer), which is a rollup plugin that generates a visual representation of the bundle.

[This](https://github.com/mermaid-js/mermaid/pull/3823) PR adds the visualizer plugin to the mermaid repo and generates 3 types of graphs.

Treemap & Sunburst are useful to see the space utilization.
Network shows us the dependency graph. It's a bit messy, so you might need to play around with the regex to clean some stuff out.

Opening the diagrams in new tab will give you a better view.

## mermaid.js

{{< iframe title="Treemap Diagram" url="/html/mermaid/old/mermaid.min.js/treemap.html" open=true >}}
{{< iframe title="Network Diagram" url="/html/mermaid/old/mermaid.min.js/network.html" >}}
{{< iframe title="Sunburst Diagram" url="/html/mermaid/old/mermaid.min.js/sunburst.html" >}}

## mermaid.core.mjs

{{< iframe title="Treemap Diagram" url="/html/mermaid/old/mermaid.core.mjs/treemap.html" open=true >}}
{{< iframe title="Network Diagram" url="/html/mermaid/old/mermaid.core.mjs/network.html" >}}
{{< iframe title="Sunburst Diagram" url="/html/mermaid/old/mermaid.core.mjs/sunburst.html" >}}

You can see that the core build contains just the core internal components. (There is some extra dependencies added, I'm not really sure why vite included it, but it's a very small fraction (7.8%), compared to 58.8% of unified build)

---

# Shrinking the bundle

## Lodash

![](/images/mermaid/lodashTreemap.png)

Lodash is a very popular utility library, and is used by mermaid to perform some operations. It is a very large library, and is used in a very small fraction of the codebase.

We could replace it with custom code, but it might not help much as lodash is already a sub-dependency of dagre and dagre-d3.

{{< figure src="/images/mermaid/lodashDependency.png" title="Lodash as sub-dependency" height=300px >}}

But is there something easier?

The tree-map tells us that it is ~28% of our bundle size. That's huge for something that's only used in 2 places & 3 test files.

{{< figure src="/images/mermaid/lodashUsage.png" title="Lodash usage in mermaid" height=300px >}}

Turns out, yes.

The network graph shows that the biggest lodash import is from `mermaidAPI.ts`.
![Lodash Import](/images/mermaid/lodashImport.png)

And when looking at the import, it's

```ts
import { isEmpty } from "lodash";
```

Whereas everywhere else, it's

```ts
import memoize from "lodash/memoize";
```

So, let's try changing that import.

```diff
- import { isEmpty } from "lodash";
+ import isEmpty from "lodash/isEmpty";
```

Build... And...

{{< iframe title="Treemap after Lodash fix" url="/html/mermaid/new/lodashFix/treemap.html" open=true >}}
{{< iframe title="Network after Lodash fix" url="/html/mermaid/new/lodashFix/network.html" >}}
{{< iframe title="Sunburst after Lodash fix" url="/html/mermaid/new/lodashFix/sunburst.html" >}}

| Bundle              | Size    | Old     | Change   | % Change |
| ------------------- | ------- | ------- | -------- | -------- |
| mermaid.core.mjs    | 1080.32 | 1080.32 | 0        | 0.00     |
| mermaid.esm.mjs     | 1951.35 | 2165.83 | \-214.48 | \-9.90   |
| mermaid.esm.min.mjs | 1429.69 | 1554.08 | \-124.39 | \-8.00   |
| mermaid.js          | 2055.7  | 2281.14 | \-225.44 | \-9.88   |
| mermaid.min.js      | 1071.37 | 1148.52 | \-77.15  | \-6.72   |

And we can see that it has reduced the bundle size by 9.9% (214.48 KiB) for the ESM build, and 9.88% (225.44 KiB) for the UMD build. There is no change in core build, as it doesn't contain any external dependencies.

| Bundle              | gzip Size | Old    | Change  | % Change |
| ------------------- | --------- | ------ | ------- | -------- |
| mermaid.core.mjs    | 218.15    | 218.15 | 0       | 0.00     |
| mermaid.esm.mjs     | 414.91    | 455.45 | \-40.54 | \-8.90   |
| mermaid.esm.min.mjs | 361.61    | 392.58 | \-30.97 | \-7.89   |
| mermaid.js          | 419.65    | 460.57 | \-40.92 | \-8.88   |
| mermaid.min.js      | 320.45    | 347.79 | \-27.34 | \-7.86   |

The gzip and minified size changes are inline with the bundle size changes, so I won't be showing them for the rest of the post. The ESM and UMD bundle size changes are also inline with each other, so I'll only be showing the `mermaid.js` bundle size changes.

| Bundle           | Size    | Old     | Change   | % Change |
| ---------------- | ------- | ------- | -------- | -------- |
| mermaid.core.mjs | 1080.32 | 1080.32 | 0        | 0.00     |
| mermaid.js       | 2055.7  | 2281.14 | \-225.44 | \-9.88   |

So just one line change reduced the bundle size by 9.88% (225.44 KiB). Awesome!

I tried using the `lodash-es` package, which is a ES module version of lodash, but it didn't help much. It actually increased the size of the bundle by 30 KiB. So let's stick with the `lodash` package.

| Bundle           | Size    | Old     | Change | % Change |
| ---------------- | ------- | ------- | ------ | -------- |
| mermaid.core.mjs | 1104.15 | 1080.32 | +23.83 | +2.22    |
| mermaid.js       | 2085.77 | 2055.7  | +30.07 | +1.46    |

But, if we were using the old `import { isEmpty } from "lodash-es";` syntax, it would have reduced the bundle size without us having to change all imports to `lodash/isEmpty`, etc.

{{< figure src="/images/mermaid/lodashSunburst.png" title="Lodash size after optimization" >}}

The sunburst diagram is a great tool to see which are the biggest components of the bundle. We can see that lodash is now 10.08% of the bundle size, and is still the biggest dependency.

---

## Dagre & Dagre-D3

As these libraries were unmaintained, [Alois Klink](https://github.com/aloisklink) raised [this PR](https://github.com/mermaid-js/mermaid/pull/3809) to replace them with [dagre-d3-es](https://github.com/tbo47/dagre-es), which shaved of another 216Kb from the `mermaid.js` bundle.

| Bundle           | Size    | Old     | Change   | % Change |
| ---------------- | ------- | ------- | -------- | -------- |
| mermaid.js       | 1839.41 | 2055.7  | \-216.29 | \-10.52  |
| mermaid.core.mjs | 1313.80 | 1080.32 | +233.48  | +21.61   |

But there's something interesting here, the core build has gone up 20% in size. Let's dig in.

{{< iframe title="Treemap after adding dagre-d3-es" url="/html/mermaid/new/before-dagre-es-fix/treemap.html" open=true >}}
{{< iframe title="Network after adding dagre-d3-es" url="/html/mermaid/new/before-dagre-es-fix/network.html" >}}
{{< iframe title="Sunburst after adding dagre-d3-es" url="/html/mermaid/new/before-dagre-es-fix/sunburst.html" >}}

So we can see that the savings came from unused stuff in dagre-d3 being tree shaken off, but a humongous lodash-es dependency was added. `lodash-es` was supposed to be treeshakeable and the solution to the problem, but it seems like it's not. So let's try to fix it.

Looking at the source, we see the following import.

```ts
import _ from "lodash-es";
```

From a blog I read earlier (don't remember which), I knew that this was a bad practice, and that we should import the specific functions we need, instead of the whole library. Or, we should do the following to enable tree-shaking.

```ts
import * as _ from "lodash-es";
```

As it's an external dependency, we'll have to raise a PR in the `dagre-d3-es` repo. But to validate the fix, we can have to

- Fork it
- Build locally
- Link the local build it in pnpm
- Link it to mermaid
- Build mermaid

Or...

- Do a find & replace in `node_modules > dagre-d3-es`
- Build mermaid

```diff
- import _ from 'lodash-es';
+ import * as _ from 'lodash-es';
```

Guess which one I did? 😅

![](/images/mermaid/lodash-es-replace.png)

| Bundle           | Initial | After dagre-es | After fix | Change   | % Change |
| ---------------- | ------- | -------------- | --------- | -------- | -------- |
| mermaid.js       | 2055.7  | 1839.41        | 1694.35   | \-361.35 | \-17.58  |
| mermaid.core.mjs | 1080.32 | 1313.80        | 1178.73   | +98.41   | +9.11    |

So, just by changing the import syntax, we were able to reduce the bundle size by 17.58% (361.35 KiB).

But the core is still up by 9.11%. What could it be?

{{< iframe title="Treemap after fixing dagre-d3-es" url="/html/mermaid/new/after-dagre-es-fix/treemap.html" open=true >}}
{{< iframe title="Network after fixing dagre-d3-es" url="/html/mermaid/new/after-dagre-es-fix/network.html" >}}
{{< iframe title="Sunburst after fixing dagre-d3-es" url="/html/mermaid/new/after-dagre-es-fix/sunburst.html" >}}

Hmm... `lodash` and `lodash-es`... 🤔
Remember when I said `lodash` is a sub-dependency, well if you look at the packages, `dagre` & `dagre-d3` were the ones importing `lodash`. Now that they're gone, `lodash` is a direct unnecessary dependency of mermaid. Let's replace it with `lodash-es`, what `dagre-d3-es` is using.

![](/images/mermaid/replace-loadsh-es-imports.png)

| Bundle     | Initial | dagre-es | fix import | lodash-es | Change | % Change |
| ---------- | ------- | -------- | ---------- | --------- | ------ | -------- |
| mermaid.js | 2055    | 1839     | 1694       | 1707      | \-348  | \-16.94  |
| core.mjs   | 1080    | 1313     | 1178       | 1105      | +25    | +2.36    |

So, core went from +9.11% to +2.36%. But `mermaid.js` went from -17.58% to -16.94%. What's going on?

{{< iframe title="Treemap after replacing lodash with lodash-es" url="/html/mermaid/new/removing-lodash/treemap.html" open=true >}}
{{< iframe title="Network after replacing lodash with lodash-es" url="/html/mermaid/new/removing-lodash/network.html" >}}
{{< iframe title="Sunburst after replacing lodash with lodash-es" url="/html/mermaid/new/removing-lodash/sunburst.html" >}}

There is still 2 lodash! Ughh...

The network graph is supposed to be used to find dependencies, but I wasn't able to find who is importing lodash. So I just randomly moved the cursor inside lodash to see if there's any "imported by" that shows up. And there was!

![](/images/mermaid/two-lodash.png)

Alois did mention in [a comment](https://github.com/mermaid-js/mermaid/pull/3809#issuecomment-1320410962) that dagre-d3-es has a `graphlib` implementation. So let's see if we can use that.

![](/images/mermaid/graphlibUsage.png)

```diff
- import graphlib from 'graphlib';
+ import * as graphlib from 'dagre-d3-es/src/graphlib';
+ import * as graphlibJson from 'dagre-d3-es/src/graphlib/json';

...

- graphlib.json.write(graph);
+ graphlibJson.write(graph);
```

After making the above changes, we can see that the bundle size has gone down by 23.97% (492 KiB). `core` is still up by 2%, _not great, not terrible_.

| Bundle     | Initial | lodash-es | graphlib | Change | % Change |
| ---------- | ------- | --------- | -------- | ------ | -------- |
| mermaid.js | 2055    | 1707      | 1563     | \-492  | \-23.97  |
| core.mjs   | 1080    | 1105      | 1106     | +26    | +2.38    |

{{< iframe title="Treemap after fixing graphlib" url="/html/mermaid/new/graphlib/treemap.html" open=true >}}
{{< iframe title="Network after fixing graphlib" url="/html/mermaid/new/graphlib/network.html" >}}
{{< iframe title="Sunburst after fixing graphlib" url="/html/mermaid/new/graphlib/sunburst.html" >}}

---

## Conclusion

So, we started with a 2.05 MiB bundle, and ended up with a 1.56 MiB bundle. That's a 23.97% reduction in bundle size. Not bad for a day's work.

Special thanks to Alois, [Thibaut (Teebo)](https://github.com/tbo47/dagre-es), [Denis Bardadym](https://github.com/btd/rollup-plugin-visualizer) and all the creators of the tools used in this post.