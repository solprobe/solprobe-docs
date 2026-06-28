---
description: Can a buyer exit this token right now, and at what cost? The cheapest pre-trade trap gate.
---

# Exit check

The cheapest pre-trade gate. Before any swap, screen whether a Solana token can actually be sold — and at what cost — to catch honeypots and trap-exits in under 7 seconds.

```
POST https://api.solprobe.xyz/exit/check      $0.01      SLA < 7s
```

## Request

```json
{ "token_address": "DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263", "size_usdc": 10 }
```

`size_usdc` optional (default 10) — the round-trip size to price.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `sellable` | boolean | Can the token be sold right now? |
| `expected_return_usdc` | number | USDC back on a round-trip of `size_usdc` |
| `exit_price_impact_pct` | number | Price impact on the sell leg |
| `route_count` | number | Distinct routes Jupiter found |
| `blockers` | string[] | Hard blockers — freeze authority active, Token-2022 non-transferable, transfer fee bps |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- A cheap yes/no exit screen before sizing or executing.
- Pair with [Quick scan](quick-scan.md) (structural) for a full pre-trade gate.

For a non-Solana agent that needs the all-in cost of exiting back to its own chain, use [Cross-chain exit check](cross-exit-check.md).
