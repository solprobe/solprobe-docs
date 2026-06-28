---
description: Pre-graduation launchpad discovery DEX scanners structurally miss.
---

# Launch radar

Surfaces Solana tokens still on the bonding curve — the launchpad stage DEX-backed trending scanners can't see — across `new_creation` and `near_completion` stages. Each candidate is graded A–F by folding its native launchpad manipulation signals through the SolProbe risk engine.

```
POST https://api.solprobe.xyz/launch/radar      $0.05      SLA < 25s
```

## Request

```json
{ "stage": "both", "limit": 15, "preset": "safe" }
```

`stage`: `new_creation` · `near_completion` · `both` (default `both`). `limit` 1–30 (default 15). Optional `preset` (`safe`/`smart-money`/`strict`), `min_smart_degen_count`, `max_rug_ratio`, `min_marketcap`, `max_marketcap`.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `launchpad_radar` |
| `tokens[].stage` | enum | `new_creation` · `near_completion` |
| `tokens[].risk_grade` | enum | A–F (same engine as Quick scan) |
| `tokens[].bonding_progress` | number | Curve fill 0–1 |
| `tokens[].smart_degen_count` | number | Smart-money holders |
| `tokens[].manipulation` | object | `{ rug_ratio, bundler_trade_rate, is_wash_trading }` |
| `tokens[].quickscan` | object \| null | Snapshot for `near_completion` (DEX footprint); `null` pre-graduation |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Bonding-curve discovery for early-entry agents.

For graduation timing, use [Graduation radar](graduation-radar.md). A discovery surface — pair with a deep scan before acting.
