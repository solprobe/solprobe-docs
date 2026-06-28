---
description: Where the smart-money cohort is deploying — pre-screened for safety.
---

# Smart money

The top tokens the smart-money cohort is buying over a chosen interval and trader-style segment, each pre-screened through the SolProbe structural safety gate. Every entry carries net smart-money flow and a distinct smart-trader count.

```
POST https://api.solprobe.xyz/scan/smart-money      $0.05      SLA < 28s
```

## Request

```json
{ "limit": 10, "interval": "7d", "trader_style": "all" }
```

`limit` 1–25 (default 10). `interval`: `1d` · `7d` · `30d` (default `7d`). `trader_style`: `all` · `risk_averse` · `risk_balancers` · `trenchers` (default `all`). All optional.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `birdeye_smart_money` |
| `tokens[].symbol` | string | Token symbol |
| `tokens[].address` | string | Base58 mint |
| `tokens[].net_flow_usd` | number | Net smart-money flow over the interval |
| `tokens[].smart_traders_no` | number | Distinct smart-money traders |
| `tokens[].quickscan` | object | Full [Quick scan](quick-scan.md) structural snapshot |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Copy-trade discovery screened for honeypots.
- Following smart-money flow into early positions.

To vet a specific wallet's track record, pair with a deep scan; to screen one token, use [Quick scan](quick-scan.md).
