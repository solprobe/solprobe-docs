---
description: >-
  SolProbe is the risk-intelligence layer for Solana tokens — an A–F safety
  grade, live market signal, and adversarial deep-dive that any agent can call
  per-request via x402. No API key, no account, no subscription.
---

# Introduction

**SolProbe is a pay-per-call Solana token risk scanner built for AI agents.** Point it at any SPL mint and get back structured JSON: a deterministic A–F structural-safety grade, a live BULLISH/BEARISH/NEUTRAL market signal, or a full adversarial deep-dive with a BUY/AVOID/WATCH/DYOR recommendation. Pay per call in USDC over [x402](access-paths/x402.md) — no key, no account, no signup.

Think of SolProbe as the **pre-trade gate** in any Solana workflow: scan first, then size and execute.

## Vision

Autonomous agents are starting to move real money on-chain — but they trade blind. The risk context a careful human gathers before aping into a token (is the mint authority revoked? is liquidity real or is this a honeypot? are the holders a handful of bundled wallets?) is scattered across explorers, dashboards, and tribal knowledge, and none of it is machine-callable in one shot.

**Our vision is a world where risk intelligence is a cheap, instant, on-demand primitive** — where any agent can verify what it's about to trade in the same breath as the trade itself, and "did you check it?" is answered by an API call, not a research session.

## Mission

**To be the structural-safety and risk layer for Solana** — giving any agent, app, or person an honest, verifiable verdict on any SPL token, available the moment they need it:

- **Honest** — deterministic structural facts (authorities, holder concentration, LP burn) are computed from live on-chain data, never hallucinated. The A–F grade is reproducible.
- **Instant** — sub-5-second structural scans, sub-30-second deep-dives, with hard SLAs.
- **Frictionless** — per-call USDC via x402 on Base or Solana. No keys, no accounts, no minimums. An agent with a funded wallet can call SolProbe in one line.
- **Everywhere agents are** — reachable as a direct HTTP endpoint, an [OpenClaw skill](access-paths/openclaw-skill.md), a [Virtuals ACP](access-paths/virtuals-acp.md) service, or a [browser](access-paths/browser.md) tool, all at price parity.

## Who is it for?

{% tabs %}
{% tab title="AI trading agents" %}
The core user. Call `/scan/quick` as a cheap structural gate before any buy or swap, `/market/intel` to read momentum before sizing, and `/scan/deep` for full due diligence on a real position. Structured JSON in, structured verdict out — no scraping, no parsing dashboards.
{% endtab %}

{% tab title="Agent builders & frameworks" %}
Building on OpenClaw, Virtuals ACP, or your own x402 client? Drop SolProbe in as a ready-made risk capability. Install the [OpenClaw skill](access-paths/openclaw-skill.md), hire the ACP agent, or hit the HTTP API directly — same services, same prices across every channel.
{% endtab %}

{% tab title="Wallets & trading apps" %}
Embed a one-call safety check into a swap flow or token page. Show users an A–F grade and the reasons behind it before they sign, with no backend of your own to maintain.
{% endtab %}

{% tab title="Humans (DYOR)" %}
Not an agent? Use the [browser](access-paths/browser.md) on `solprobe.xyz` — connect a wallet, pay per scan, and get the same structured intelligence agents do, without writing any code.
{% endtab %}
{% endtabs %}

## What you get

| Service | Price | Returns |
|---|---|---|
| **Quick Scan** | $0.02 | A–F structural-safety grade — authorities, holder concentration, LP status |
| **Market Intel** | $0.20 | BULLISH/BEARISH/NEUTRAL signal + buy/sell pressure, volume, volatility |
| **Deep Dive** | $0.50 | Adversarial report — wallet clustering, wash trading, dev history + recommendation |

{% hint style="info" %}
New here? Start with [**Getting started**](getting-started.md) to fund a wallet and make your first call, or jump to [**Access paths**](access-paths/README.md) to pick the integration that fits you.
{% endhint %}
