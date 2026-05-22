---
description: Adversarial deep-dive — wallet clustering, wash trading, dev history, and a recommendation.
---

# Deep dive

Full due diligence on a Solana token. Everything in the [Quick scan](quick-scan.md) plus an adversarial risk engine: wallet clustering, dev-wallet history, launch pattern, wash-trading detection, and a structured recommendation.

```
POST https://api.solprobe.xyz/scan/deep      $0.50      SLA < 30s
```

## Request

```json
{ "token_address": "DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `risk_grade` | enum | `A` · `B` · `C` · `D` · `F` |
| `risk_breakdown` | object | `{ contract_risk, liquidity_risk, market_risk, behavioral_risk }` each `LOW` · `MEDIUM` · `HIGH` |
| `is_honeypot` | boolean | Honeypot detected |
| `wallet_analysis` | object | `{ clustered_wallets, insider_control_percent, dev_wallet_linked }` |
| `dev_wallet_analysis` | object | `{ address, sol_balance, created_tokens_count, previous_rugs }` |
| `launch_pattern` | enum | `STEALTH_LAUNCH` · `FAIR_LAUNCH` · `UNKNOWN` |
| `sniper_activity` | enum | `LOW` · `MEDIUM` · `HIGH` |
| `liquidity_lock_status` | object | `{ locked, lock_duration_days, locked_pct }` |
| `trading_pattern` | object | `{ buy_sell_ratio_1h, unique_buyers_24h, wash_trading_score }` |
| `pump_fun_launched` | boolean | Launched via pump.fun |
| `bundled_launch_detected` | boolean | Bundled-launch signature |
| `momentum_score` | number | Composite momentum |
| `recommendation` | object | `{ action: AVOID \| WATCH \| CONSIDER \| DYOR, reason, confidence, time_horizon }` |
| `key_drivers` | object[] | The factors that most shaped the verdict |
| `full_risk_report` | string | Narrative report |

Plus the standard [response envelope](README.md#response-envelope).

{% hint style="success" %}
`recommendation.action` defaults to `DYOR` when confidence is insufficient — SolProbe never forces a BUY/AVOID it can't stand behind.
{% endhint %}

## When to use

- Before committing a meaningful position.
- When a [Quick scan](quick-scan.md) is ambiguous and you need adversarial context (clustering, wash trading, dev history).
