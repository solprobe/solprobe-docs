---
description: Premium momentum scoring on the about-to-graduate shortlist.
---

# Graduation momentum

The premium graduation feed. Takes the about-to-graduate shortlist and scores the **momentum** of the top N candidates (0–100) by folding bonding-curve velocity, live market signal, an exit-feasibility gate, and dev-wallet risk — the lighter half of the full trade battery, no deep dive.

```
POST https://api.solprobe.xyz/graduation/momentum      $0.40      SLA < 50s
```

## Request

```json
{ "min_bonding_progress": 0.7, "min_grade": "C", "enrich_count": 5 }
```

`min_bonding_progress` 0–1 (default 0.70). Optional `min_grade` (A–F floor). `enrich_count` 1–10 (default 5) — how many top candidates to score.

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `graduation_momentum` |
| `tokens[].momentum.momentum_score` | number | 0–100 |
| `tokens[].momentum.momentum_label` | enum | `HOT` · `HEATING` · `COOLING` · `FLAT` |
| `tokens[].momentum.market_signal_source` | string | `market_intel` or on-curve trade flow |
| `tokens[].momentum.cited_factors` | object[] | Scored drivers |
| `tokens[].momentum.component_status` | object | Which inputs were available |

Plus the standard [response envelope](README.md#response-envelope).

{% hint style="info" %}
A high score reflects **buying velocity + market signal**, not safety or a price prediction.
{% endhint %}

## When to use

- Ranking graduation candidates by buying velocity for execution-ready agents.

For the cheaper imminence-only cut, use [Graduation radar](graduation-radar.md).
