---
description: Pre-screened trending tokens — the hot list, run through the safety gate.
---

# Trending

The top trending Solana tokens by volume and liquidity, each pre-screened through the SolProbe structural safety gate so you get "what's hot **and** not obviously a honeypot" in one call. LSTs are filtered out.

```
POST https://api.solprobe.xyz/scan/trending      $0.02      SLA < 28s
```

## Request

```json
{ "limit": 25, "sort_by": "rank" }
```

`limit` 1–25 (default 25). `sort_by`: `rank` · `volume24hUSD` · `liquidity` (default `rank`). All optional.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `birdeye_trending` |
| `tokens[].rank` | number | Trending rank |
| `tokens[].symbol` | string | Token symbol |
| `tokens[].address` | string | Base58 mint |
| `tokens[].price_usd` | number \| null | Current price |
| `tokens[].liquidity_usd` | number \| null | Pool liquidity |
| `tokens[].quickscan` | object | Full [Quick scan](quick-scan.md) structural snapshot (A–F grade, authority flags, LP burn, top-10 %) |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- Discovery feed for momentum / rotation agents.
- Seeding a watchlist with structurally-screened candidates.

For pre-graduation tokens trending can't see, use [Launch radar](launch-radar.md). To vet one token, use [Quick scan](quick-scan.md).
