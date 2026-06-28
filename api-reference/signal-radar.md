---
description: What's converging on-chain right now — a weighted convergence score.
---

# Signal radar

Ranks Solana tokens by a weighted **convergence score** — how many distinct bullish on-chain signals (smart-money buys, community takeover, all-time-high, price spikes, platform calls) are co-firing for a token right now. Each top entry is structurally enriched.

```
POST https://api.solprobe.xyz/signal/radar      $0.04      SLA < 25s
```

## Request

```json
{ "limit": 10, "min_convergence": 4.5 }
```

`limit` 1–20 (default 10). Optional `mc_min` / `mc_max` (market cap USD) and `min_convergence` (weighted score). All optional.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `convergence_signals` |
| `tokens[].convergence_score` | number | Weighted score |
| `tokens[].signal_breakdown` | object[] | `{ type, name, count, weight }` per firing signal |
| `tokens[].distinct_bullish_types` | number | Distinct signals co-firing |
| `tokens[].quickscan` | object | Full [Quick scan](quick-scan.md) snapshot |
| `tokens[].flags` | string[] | Neutral manipulation flags |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Attention / conviction radar for setup-seeking agents.

A conviction surface, not a price prediction — pair with [Deep dive](deep-dive.md) before acting.
