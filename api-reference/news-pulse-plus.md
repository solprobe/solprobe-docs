---
description: Synthesis with cohort attribution — ecosystem / analyst / degen voices.
---

# News pulse+

Synthesis with **cohort attribution** — splits the conversation by ecosystem, analyst, and degen voices, so an agent sees *who* is saying what rather than a single flattened sentiment.

```
POST https://api.solprobe.xyz/news/pulse_plus      $0.10      SLA < 12s
```

## Request

```json
{ "symbol": "BONK" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `signal` | enum | Aggregate `BULLISH` · `BEARISH` · `NEUTRAL` · `MIXED` |
| `cohorts` | object | Per-cohort sentiment: `ecosystem` / `analyst` / `degen` |
| `synthesis` | string | Synthesis of the cohort split |
| `tweet_count` | number | Tweets analysed |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Weighting sentiment by who is voicing it (analyst conviction vs degen hype).

For the deepest structured report with risks + watch list, use [News report](news-report.md).
