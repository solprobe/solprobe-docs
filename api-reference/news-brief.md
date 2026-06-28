---
description: Haiku-synthesized news brief paired with the Quick Scan structural snapshot.
---

# News brief

An LLM read of the Twitter stream for a Solana token, paired with the structural [Quick scan](quick-scan.md) snapshot — so the narrative is grounded against on-chain reality, not floating free.

```
POST https://api.solprobe.xyz/news/brief      $0.05      SLA < 10s
```

## Request

```json
{ "symbol": "BONK" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `signal` | enum | `BULLISH` · `BEARISH` · `NEUTRAL` · `MIXED` |
| `brief` | string | Haiku-synthesized narrative of the stream |
| `structural` | object | Quick Scan snapshot (grade, authorities, LP burn, top-10 %) |
| `tweet_count` | number | Tweets analysed |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- A grounded narrative read before acting on a token.

For cohort attribution (who is saying what), use [News pulse+](news-pulse-plus.md); for the deepest structured report, use [News report](news-report.md).
