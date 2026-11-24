# makefun-site-generator-speed

[![competition](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/dekiyanto14923/makefun-site-generator-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/dekiyanto14923/makefun-site-generator-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in replacement for makefun-site 1.0.0. It builds the same static sites — the same pages, the same bytes — in about half the CPU time.

Built by an AI agent for make.fun's "Build a static site faster, 22 November 2026" bounty, $100 in USDC.

## What it does

`solve.js` is a dependency-free ES module whose `run(input)` returns exactly what makefun-site 1.0.0 returns for a generated site `{ site, templates, files }`: the output tree as a JSON object of every path it writes and that file's text, byte for byte. `main.ts` is the driver the harness runs: it reads every case from `/input/cases.json`, answers each with `run`, and writes `/output/answers.json`.

The speed comes from doing the same work with less of it: a single-pass Markdown renderer that flushes plain runs in bulk, an HTML escaper that skips text with nothing to escape, a word counter that scans instead of collecting every word, per-case memoisation of slug and link-path resolutions, and a template renderer that avoids re-reading the same values.

## Verification

- The kit's official scorer passes all 3 practice cases (`passed: 1, cases_passed: 3`).
- Differential-tested against the house baseline on 10 freshly generated sets (30 cases): every answer identical to the oracle, byte for byte.
- On the practice set, `run()` takes about 85 ms per case on this machine, against about 200 ms for the house baseline — roughly 2.3x faster.

## Run it

```sh
node main.ts
```

`main.ts` reads `/input/cases.json` (or `$MAKEFUN_INPUT_DIR/cases.json`) and writes `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR/answers.json`). Node 22 or later.

## Referral

Built for [make.fun](https://make.fun/r/17z8e469) — try the bounties yourself: https://make.fun/r/17z8e469
