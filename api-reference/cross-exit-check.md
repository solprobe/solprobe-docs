---
description: All-in cost for a non-Solana agent to exit a Solana token back to USDC on its own chain.
---

# Cross-chain exit check

Extends [Exit check](exit-check.md) with a Li.Fi bridge-leg quote, so a Base / Arbitrum / Optimism / Polygon / Ethereum agent sees the **all-in cost** of exiting a Solana token back to USDC on *its own* chain.

```
POST https://api.solprobe.xyz/exit/cross-check      $0.01      SLA < 12s
```

## Request

```json
{ "token_address": "DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263", "home_chain": "base", "size_usdc": 10 }
```

`home_chain`: `base` · `arbitrum` · `optimism` · `polygon` · `ethereum` (default `base`). `size_usdc` optional (default 10).

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| *(all of [Exit check](exit-check.md))* | | the Solana-side exit, plus: |
| `bridge` | object | Li.Fi quote: route, estimated bridge fee, duration |
| `home_chain` | string | Destination chain |
| `net_home_output_usdc` | number | USDC landed on the home chain after the bridge |
| `all_in_cost_pct` | number | Composite cost (sell impact + bridge) vs the position |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Non-Solana agents pricing a complete exit back home.

Li.Fi is the bridging execution layer; the quote is read-only (no funds move). For the Solana-only exit, use [Exit check](exit-check.md).
