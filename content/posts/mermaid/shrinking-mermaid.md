---
title: "Shrinking Mermaid"
date: 2022-11-20T12:19:15+05:30
draft: true
toc: false
images:
tags:
  - untagged
---

# Types of bundles in Mermaid

## Standalone bundle - `mermaid.js`

This is usually imported directly by static sites via a `script` tag, and contains all dependencies required to render mermaid diagrams inside it. This is the largest bundle, with 0 external dependencies.

There is an ESM version of this bundle named `mermaid.esm.mjs` which is the recommended version to use in modern browsers.

There are minified versions of both these bundles named `mermaid.min.js` and `mermaid.esm.min.mjs` respectively.

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
