# Fast makefun-site drop-in

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![Rank](https://make.fun/badge/site-generator-speed-01-run-20261122/cihuy13/fast-makefun-site-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![Reward](https://make.fun/badge/site-generator-speed-01-run-20261122/cihuy13/fast-makefun-site-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0, entered in
[Build a static site faster, 22 November 2026](https://make.fun/bounty/site-generator-speed-01-run-20261122).

`solve.js` is a dependency-free ES module whose `run(input)` returns, for every
case's input, exactly the answer makefun-site 1.0.0 returns — byte for byte.
`main.ts` is the harness driver: it reads every case from `/input/cases.json`,
answers each with `run`, and writes `/output/answers.json`.

## Method

Own implementation of makefun-site's own dialect (front matter, template
dialect, Markdown subset, slug rule, report), written for speed:

- single-pass Markdown scan with bulk HTML escaping (no per-character regex)
- ASCII fast path for slugify (NFKD only when non-ASCII is present)
- memoised slug/date lookups inside a case; templates parsed once per case
- string building with push/join, no repeated re-scans of the same text

No cache is shared across cases: each case is answered alone.
