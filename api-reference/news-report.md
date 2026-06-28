---
description: Sonnet-grade structured news report — takes, synthesis, risks, and a filtered watch list.
---

# News report

The deepest read on a Solana token's news flow — a Sonnet-grade structured report with key takes, a synthesized narrative, explicit risks, and a watch list (with invented-token filtering so hallucinated tickers don't leak through).

```
POST https://api.solprobe.xyz/news/report      $0.25      SLA < 25s
```

## Request

```json
{ "symbol": "BONK" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `signal` | enum | `BULLISH` · `BEARISH` · `NEUTRAL` · `MIXED` |
| `takes` | string[] | Key takeaways |
| `synthesis` | string | Narrative synthesis |
| `risks` | string[] | Risks called out explicitly |
| `watch_list` | string[] | Related tickers — invented-id filtered |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Pre-position due diligence on the narrative side, in one structured call.

For a cheaper read, use [News brief](news-brief.md) or [News pulse](news-pulse.md).
