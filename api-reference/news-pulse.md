---
description: Lexicon-only Twitter pulse for a Solana token — the cheapest read on live sentiment.
---

# News pulse

The cheapest sentiment read. A lexicon-only pulse of the live Twitter cashtag stream for a Solana token — a bullish/bearish/neutral signal with counts and top terms, fully deterministic.

```
POST https://api.solprobe.xyz/news/pulse      $0.01      SLA < 8s
```

## Request

```json
{ "symbol": "BONK" }
```

`symbol` optional — a cashtag or mint. Omit for broad mode (curated Solana-Twitter ecosystem cohort).

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `mode` | enum | `symbol` · `broad` |
| `signal` | enum | `BULLISH` · `BEARISH` · `NEUTRAL` · `MIXED` |
| `bull_count` / `bear_count` / `neutral_count` | number | Tweet sentiment tallies |
| `top_terms` | string[] | Most-mentioned terms |
| `tweet_count` | number | Tweets analysed |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- A fast, cheap, deterministic sentiment sweep.

For a synthesized read grounded against on-chain structure, use [News brief](news-brief.md).
