---
description: Live market signal — pumping or dumping, with the numbers behind it.
---

# Market intel

A real-time trading signal for a Solana token: a BULLISH / BEARISH / NEUTRAL call backed by price action, volume, buy/sell pressure, and whale activity. Use it before sizing or executing a position.

```
POST https://api.solprobe.xyz/market/intel      $0.20      SLA < 10s
```

## Request

```json
{ "token_address": "DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `signal` | enum | `BULLISH` · `BEARISH` · `NEUTRAL` |
| `signal_subtype` | string | More specific characterization of the signal |
| `buy_sell_ratio` | number | Buy vs sell flow |
| `buy_pressure` / `sell_pressure` | enum | `HIGH` · `MEDIUM` · `LOW` |
| `volatility` | enum | `LOW` · `MEDIUM` · `HIGH` |
| `token_health` | enum | `ACTIVE` · `LOW_ACTIVITY` · `DECLINING` · `ILLIQUID` · `DEAD` |
| `current_price_usd` | number | Latest price |
| `price_change_1h_pct` / `price_change_24h_pct` | number | Momentum |
| `volume_1h_usd` / `volume_24h_usd` | number | Traded volume |
| `liquidity_usd` | number | Pool liquidity |
| `large_txs_last_hour` | number | Whale-sized transactions |
| `market_summary` | string | Plain-English read |

Plus the standard [response envelope](README.md#response-envelope).

## When to use

- To gauge entry timing once a token has passed a [Quick scan](quick-scan.md).
- To monitor momentum on a position you already hold.

{% hint style="info" %}
Market intel is about **price action**, not safety. Always run a [Quick scan](quick-scan.md) first to confirm the token is structurally sound.
{% endhint %}
