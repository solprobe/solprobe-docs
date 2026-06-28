---
description: Per-call pricing for every SolProbe service. Same price on every channel.
---

# Pricing

SolProbe is **pay-per-call** in USDC. No subscription, no minimums, no monthly fee — you pay only for the calls you make. Prices are **identical across every** [**access path**](access-paths/README.md) (x402, OpenClaw, Virtuals ACP, browser) and on both rails (Base and Solana).

| Service | Price | Endpoint |
| --- | --- | --- |
| Quick scan | **$0.02** | `POST /scan/quick` |
| Market intel | **$0.20** | `POST /market/intel` |
| Deep dive | **$0.50** | `POST /scan/deep` |
| Trending | **$0.02** | `POST /scan/trending` |
| Smart money | **$0.05** | `POST /scan/smart-money` |
| Signal radar | **$0.04** | `POST /signal/radar` |
| Launch radar | **$0.05** | `POST /launch/radar` |
| Graduation radar | **$0.06** | `POST /graduation/radar` |
| Graduation momentum | **$0.40** | `POST /graduation/momentum` |
| Exit check | **$0.01** | `POST /exit/check` |
| Cross-chain exit check | **$0.01** | `POST /exit/cross-check` |
| Wallet intel | **$0.10** | `POST /wallet/intel` |
| News pulse | **$0.01** | `POST /news/pulse` |
| News brief | **$0.05** | `POST /news/brief` |
| News pulse+ | **$0.10** | `POST /news/pulse_plus` |
| News report | **$0.25** | `POST /news/report` |
| Trade quote | **Free** | `POST /trade/quote` |
| Trade execute | **$0.15** | `POST /trade/execute` (charged on commit only) |

All amounts are in USDC (6 decimals). Free, unpaywalled routes — `/health`, `/trade/status`, `/trade/pairs`, `/trade/currencies`, and all [discovery surfaces](discovery-and-identity.md) — cost nothing.

{% hint style="info" %}
Prices are authoritative at the live `402` challenge and in [`/openapi.json`](https://api.solprobe.xyz/openapi.json) (`x-payment-info`). If this page ever disagrees, trust the live endpoint.
{% endhint %}

## Example costs

| Workflow | Calls | Cost |
| --- | --- | --- |
| Pre-trade safety gate | `quick` | $0.02 |
| Gate + momentum read | `quick` + `market` | $0.22 |
| Full due diligence | `quick` + `market` + `deep` | $0.72 |
| Scan then swap | `quick` + `trade/quote` (free) + `trade/execute` | $0.17 |
