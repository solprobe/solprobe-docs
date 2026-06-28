---
description: Deep behavioural & risk profile for any Solana wallet — copy-trade and counterparty vetting.
---

# Wallet intel

A behavioural and risk profile for any Solana wallet — win rate, realized PnL, hold time, funding origin, and a structured risk verdict. Use it to decide whether to copy-trade a wallet, or to screen a dev / whale / counterparty before acting.

```
POST https://api.solprobe.xyz/wallet/intel      $0.10      SLA < 9s
```

## Request

```json
{ "wallet_address": "BybBpqdT5fmmyv61eXZ14Z1PEfvbv4yjGNezybQw7XAF" }
```

## Response (key fields)

| Field | Type | Description |
| --- | --- | --- |
| `win_rate_pct` | number | Share of profitable positions |
| `realized_pnl_usd` | number | Realized profit/loss |
| `avg_hold_time` | string | Typical holding duration |
| `total_trades` | number | Lifetime trade count |
| `funding_origin` | enum | CEX · mixer · fresh-wallet · … |
| `behaviour_style` | enum | sniper · flipper · momentum · hodler · bot · pro_trader |
| `copy_trade_worthiness` | object | Recommendation + sample size |
| `verdict` | enum | `LOW_RISK` · `HIGH_RISK` · `UNKNOWN` |

Plus the standard [response envelope](README.md#response-envelope). Backed by aggregated on-chain wallet analytics, so win-rate and PnL stay robust even for high-volume wallets an RPC tx-cap would undercount.

## When to use

- Deciding whether to copy-trade or follow a wallet.
- Screening a dev or whale before acting on their token.
