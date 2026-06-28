---
description: The flagship — end-to-end trade discovery + decision-support in one call.
---

# Suggest trade

The flagship decision-support primitive. In one call the engine discovers a candidate and tells you how to act on it: it fans out to the discovery radars, ranks a shortlist, picks the strongest, and runs the full battery on it — folding everything into a single recommendation. **Decision-support only** — no custody, quote, or execution.

```
POST https://api.solprobe.xyz/trade/suggest      $0.60      SLA < 50s
```

## Request

```json
{ "risk_appetite": "balanced", "source": "both" }
```

All optional. Omit everything to run full discovery. `risk_appetite`: `conservative` · `balanced` · `aggressive`. `source`: `signal` · `launch` · `both`. Optional `mc_min` / `mc_max`.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `recommendation.action` | enum | `AVOID` · `WATCH` · `CONSIDER` · `DYOR` |
| `recommendation.conviction` | number | 0–100 |
| `recommendation.suggested_size_usd` | number \| null | Position-size hint |
| `recommendation.cited_factors` | object[] | Scored drivers behind the call |
| `recommendation.trade_plan` | object \| null | `slippage_bps`, `max_price_impact_pct`, est. round-trip exit cost, stop-loss hint |
| `selection.candidate` | object \| null | The chosen token |
| `selection.why_selected` | string | Why it won |
| `selection.shortlist` | object[] | What else was in contention |

Plus the standard [response envelope](README.md#response-envelope).

{% hint style="info" %}
The recommendation is **rule-derived** from the underlying scans, never a free-form opinion. Hard gates (not-sellable / freeze / grade-F / rug) force `AVOID`.
{% endhint %}

## How it works

One call folds the whole stack: the [signal](signal-radar.md) + [launch](launch-radar.md) radars for discovery, then [deep dive](deep-dive.md), market signal, [exit check](exit-check.md), dev-wallet risk ([wallet intel](wallet-intel.md)), and social sentiment ([news brief](news-brief.md)) on the top pick.

## When to use

- "Find me something worth a position and tell me how to size it."

To **execute**, pair with [Trade](trade.md) — this endpoint never signs or broadcasts.
