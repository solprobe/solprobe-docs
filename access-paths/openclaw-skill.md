---
description: Add SolProbe to an OpenClaw agent as a one-URL skill.
---

# OpenClaw skill

SolProbe ships as an [OpenClaw](https://openclaw.ai) skill, so an OpenClaw agent gets all three scanners as native capabilities. Payment rides on x402 automatically — the agent just needs a funded wallet.

## Install

{% tabs %}
{% tab title="OpenClaw UI" %}
1. Open your OpenClaw dashboard → **Skills → Add Skill**.
2. Paste the raw skill URL:

```
https://raw.githubusercontent.com/solprobe/solprobe-skills/main/skills/solprobe.skill.md
```
{% endtab %}

{% tab title="Manual" %}
Copy the contents of [`skills/solprobe.skill.md`](https://github.com/solprobe/solprobe-skills/blob/main/skills/solprobe.skill.md) into your OpenClaw skills directory.

SolProbe also serves the canonical copy from its own host:

```
https://api.solprobe.xyz/solprobe.skill.md
```
{% endtab %}
{% endtabs %}

## What the agent gets

| Skill action | Endpoint | Price |
| --- | --- | --- |
| Quick scan | `POST /scan/quick` | $0.02 |
| Market intel | `POST /market/intel` | $0.20 |
| Deep dive | `POST /scan/deep` | $0.50 |

Each takes a Solana SPL **mint address** (`token_address`, base58, 32–44 chars) and returns the same structured JSON described in the [API reference](../api-reference/README.md).

## Payment setup

The only prerequisite is a wallet funded with **USDC on Base or Solana** — no API key, account, or signup. OpenClaw negotiates the `402` challenge and signs the payment automatically once the wallet is funded. See the [Payment guide](../payment-guide.md).

{% hint style="warning" %}
The v1 skill covers the scanners. The two-phase BYOW [trade](../api-reference/trade.md) flow isn't in the skill yet — use [x402](x402.md) or [Virtuals ACP](virtuals-acp.md) for swaps.
{% endhint %}

## Source

The skill is open source in [**github.com/solprobe/solprobe-skills**](https://github.com/solprobe/solprobe-skills) (MIT), alongside an install README and an x402 payment guide.
