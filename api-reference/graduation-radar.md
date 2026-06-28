---
description: Tokens about to graduate off the bonding curve, ranked by imminence.
---

# Graduation radar

The graduation-imminence cut of [Launch radar](launch-radar.md). Takes the `near_completion` stage, keeps candidates above a bonding-progress threshold, and ranks by how close they are to graduating. Each entry keeps its A–F grade and manipulation flags, plus a fill-rate ETA.

```
POST https://api.solprobe.xyz/graduation/radar      $0.06      SLA < 25s
```

## Request

```json
{ "min_bonding_progress": 0.7, "min_grade": "C", "limit": 15 }
```

`min_bonding_progress` 0–1 (default 0.70). Optional `min_grade` (A–F floor). `limit` 1–30 (default 15).

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `source` | string | `graduation_radar` |
| `tokens[].bonding_progress` | number | Curve fill 0–1 (ranked desc) |
| `tokens[].fill_rate_pct_per_min` | number | Average fill rate |
| `tokens[].est_minutes_to_graduation` | number | Average-rate ETA estimate |
| `tokens[].risk_grade` | enum | A–F |
| `tokens[].quickscan` | object | Full [Quick scan](quick-scan.md) snapshot |

Plus the standard [response envelope](README.md#response-envelope).

{% hint style="info" %}
`est_minutes_to_graduation` is an **average-rate** estimate, not live momentum.
{% endhint %}

## When to use

- Catching the graduation moment for timing agents.

For velocity-scored ranking, use [Graduation momentum](graduation-momentum.md).
