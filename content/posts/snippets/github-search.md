---
title: "Your queryable, public, GitHub history"
date: 2024-04-23T19:53:31+05:30
draft: false
toc: false
images:
tags:
  - GitHub
  - clickhouse
  - activity
---

I wanted to find out what all Open Source projects I had contributed to, to post it in my company's [website.](https://10xminds.dev)

My GitHub profile said "6,219 contributions in the last year, to X,Y,Z and 34 Other repositories". But which all? Were there any worth bragging about?

TL;DR Use [ClickHouse.](https://play.clickhouse.com/play?user=play#U0VMRUNUIAogICAgUFIucmVwb19uYW1lLAogICAgSUZOVUxMKFcuc3RhcnMsIDApIGFzIHN0YXJzCkZST00gCiAgICAoCiAgICAgICAgU0VMRUNUIHJlcG9fbmFtZQogICAgICAgIEZST00gZ2l0aHViX2V2ZW50cyAKICAgICAgICBXSEVSRSBhY3Rvcl9sb2dpbiA9ICdzaWRoYXJ0aHY5NicgCiAgICAgICAgICAgIEFORCBldmVudF90eXBlID0gJ1B1bGxSZXF1ZXN0RXZlbnQnIAogICAgICAgICAgICBBTkQgcmVwb19uYW1lIE5PVCBMSUtFICclc2lkaGFydGh2OTYlJwogICAgICAgIEdST1VQIEJZIHJlcG9fbmFtZQogICAgKSBQUgpMRUZUIEpPSU4gCiAgICAoCiAgICAgICAgU0VMRUNUIAogICAgICAgICAgICByZXBvX25hbWUsIAogICAgICAgICAgICBjb3VudCgpIEFTIHN0YXJzIAogICAgICAgIEZST00gZ2l0aHViX2V2ZW50cyAKICAgICAgICBXSEVSRSBldmVudF90eXBlID0gJ1dhdGNoRXZlbnQnIAogICAgICAgIEdST1VQIEJZIHJlcG9fbmFtZSAKICAgICkgVyBPTiBQUi5yZXBvX25hbWUgPSBXLnJlcG9fbmFtZQpPUkRFUiBCWSBzdGFycyBERVNDOwo=)

ChatGPT didn't have any useful suggestions, apart from "Check your GitHub Profile", "Check your Email", "Check your local repos", "Check a defunct aggregation tool", duh!

But that last one did ring a bell in my head. Few weeks back, when the Open Source community was shook by the backdoor in XZ, I remember seeing a GitHub activity histogram of the bad actor [somewhere in HN](https://news.ycombinator.com/item?id=39905375). I had played with that tool for a bit, and was impressed by it. Thankfully, I had it in my bookmarks, so I started playing around.

## Clickhouse

Running this gives all my public activity. Every single comment, PR, issue, like, start, damn!

```sql
SELECT *
FROM   github_events
WHERE  actor_login = 'sidharthv96'
ORDER  BY file_time DESC
```

Looking at the columns, `event_type`, `repo_name` and `action` seems like what I need.

To get all the PRs I've ever opened in a public repo, I can use.

```sql
SELECT *
FROM   github_events
WHERE  actor_login = 'sidharthv96'
       AND event_type = 'PullRequestEvent'
       AND action <> 'closed'
ORDER  BY file_time DESC
```

And we can get the count of PRs in each repo with this.

```sql
SELECT repo_name,
       Count() AS prs
FROM   github_events
WHERE  actor_login = 'sidharthv96'
       AND event_type = 'PullRequestEvent'
       AND action <> 'closed'
GROUP  BY repo_name
ORDER  BY prs DESC
```

But there are lots of my private repos in there, which we don't really need. So we can remove them.

```sql
 SELECT repo_name,
       Count() AS prs
FROM   github_events
WHERE  actor_login = 'sidharthv96'
       AND event_type = 'PullRequestEvent'
       AND action <> 'closed'
       AND repo_name NOT LIKE '%sidharthv96%'
GROUP  BY repo_name
ORDER  BY prs DESC
```

Combining it with a query to get stars of each repo (thanks ChatGPT), we finally get this, that ranks each repo I've ever raised a PR to, by star count.

```sql
SELECT PR.repo_name,
    IFNULL(W.stars, 0) as stars
FROM
    (
        SELECT repo_name
        FROM github_events
        WHERE actor_login = 'sidharthv96'
            AND event_type = 'PullRequestEvent'
						AND action <> 'closed'
            AND repo_name NOT LIKE '%sidharthv96%'
        GROUP BY repo_name
    ) PR
LEFT JOIN
    (
        SELECT
            repo_name,
            count() AS stars
        FROM github_events
        WHERE event_type = 'WatchEvent'
        GROUP BY repo_name
    ) W ON PR.repo_name = W.repo_name
ORDER BY stars DESC;

```

## Final result

I did notice the star counts are not accurate, but it's good enough to get a rough idea.
At the time of writing, mermaid has 66.9k start, but it shows 41.8k in clickhouse.

| repo_name                                   | stars |
| ------------------------------------------- | ----- |
| denoland/deno                               | 78062 |
| strapi/strapi                               | 63605 |
| microsoft/playwright                        | 62443 |
| gohugoio/hugo                               | 62324 |
| microsoft/TypeScript                        | 56603 |
| prettier/prettier                           | 47052 |
| DefinitelyTyped/DefinitelyTyped             | 45203 |
| mermaid-js/mermaid                          | 41838 |
| airbnb/lottie-android                       | 37761 |
| traefik/traefik                             | 18301 |
| sveltejs/kit                                | 18184 |
| typescript-eslint/typescript-eslint         | 15130 |
| encode/httpx                                | 12355 |
| vitest-dev/vitest                           | 11684 |
| utterance/utterances                        | 8866  |
| dankogai/js-base64                          | 4391  |
| js-org/js.org                               | 4303  |
| githubsaturn/captainduckduck                | 3771  |
| mermaid-js/mermaid-live-editor              | 3484  |
| open-telemetry/opentelemetry-js             | 2407  |
| mermaid-js/mermaid-cli                      | 1959  |
| Homebrew/formulae.brew.sh                   | 1506  |
| sdras/vue-vscode-snippets                   | 1403  |
| pqrs-org/KE-complex_modifications           | 1297  |
| Track3/hermit                               | 1289  |
| tsedio/tsed                                 | 1169  |
| jest-community/eslint-plugin-jest           | 1157  |
| gohugoio/hugoDocs                           | 1148  |
| mongodb/homebrew-brew                       | 976   |
| Chevrotain/chevrotain                       | 904   |
| IEEEKeralaSection/rescuekerala              | 657   |
| ArtiomTr/jest-coverage-report-action        | 498   |
| kr1sp1n/node-vault                          | 453   |
| langium/langium                             | 443   |
| testing-library/testing-library-docs        | 406   |
| cloudevents/sdk-javascript                  | 315   |
| irshadshalu/music-grid                      | 274   |
| MacFJA/svelte-persistent-store              | 227   |
| HTTP-APIs/hydrus                            | 220   |
| YuriCosta/WhatsApp-GD-Extractor-Multithread | 180   |
| inversify/inversify-binding-decorators      | 175   |
| Homebrew/brew.sh                            | 121   |
| whichjdk/whichjdk.com                       | 114   |
| jihchi/mermaid.ink                          | 93    |
| scaleway/docs-content                       | 74    |
| ttarnowski/ts-sinon                         | 66    |
| Rich-Harris/port-authority                  | 57    |
| tbo47/dagre-es                              | 30    |
| tsedio/tsed-cli                             | 23    |
| caprover/caprover-website                   | 17    |
| ryansolid/create-solid                      | 13    |
| Mermaid-Chart/vscode-mermaid-chart          | 11    |
| mermaid-js/docs                             | 10    |
| irshadshalu/Nokia_Composer_Music_Arduino    | 10    |
| degordian/avro-to-typescript                | 10    |
| TurgenSec/standards                         | 1     |
| Mermaid-Chart/plugins                       | 1     |
| JenningsWilliam/mermaid                     | 0     |
| ArtiomTr/jest-coverage-report-action-test   | 0     |
| SillyCoon/unicode-lookup                    | 0     |
