---
description: Every way to reach SolProbe — and how to choose the right one.
---

# Overview

SolProbe runs one engine behind several front doors. The **services and prices are identical** across every path — pick the one that fits how you (or your agent) already work.

## Quick comparison

| Access path | Best for | Payment | How you reach it |
| --- | --- | --- | --- |
| [**x402**](x402.md) | Agents & apps making direct, low-latency HTTP calls | Per-call USDC (Base or Solana) | `POST https://api.solprobe.xyz/...` |
| [**OpenClaw skill**](openclaw-skill.md) | Agents running on OpenClaw | Per-call USDC via x402 | Install the skill URL |
| [**Virtuals ACP**](virtuals-acp.md) | Agents in the Virtuals ecosystem wanting escrow | USDC via ACP escrow | Hire the SolProbe ACP agent |
| [**Browser**](browser.md) | Humans doing manual DYOR | Per-call USDC, wallet-connect | [solprobe.xyz](https://solprobe.xyz) |

{% hint style="info" %}
**x402 is the foundation.** The OpenClaw skill and the browser both pay over x402 under the hood; Virtuals ACP is a parallel escrow channel at the same prices. Whatever path you choose, you're hitting the same scanners.
{% endhint %}

## Which should I choose?

{% tabs %}
{% tab title="I'm an AI agent" %}
Call **x402 directly** — it's the lowest-latency, most flexible path. Use an x402 client library (e.g. `@x402/fetch`) so the `402 → sign → retry` handshake is automatic. See [Getting started](../getting-started.md).
{% endtab %}

{% tab title="I build agents" %}
- On **OpenClaw**? Install the [OpenClaw skill](openclaw-skill.md) — one URL and your agent gets all three scanners.
- Already integrated with **Virtuals ACP**? Hire the [ACP agent](virtuals-acp.md) and keep your escrow flow.
- Rolling your own stack? Hit [x402](x402.md) directly.
{% endtab %}

{% tab title="I run a wallet or app" %}
Embed [x402](x402.md) calls into your swap or token-detail flow to show users an A–F safety grade before they sign. No backend of your own required.
{% endtab %}

{% tab title="I'm a human (DYOR)" %}
Use the [browser](browser.md) at [solprobe.xyz](https://solprobe.xyz): connect a wallet, pay per scan, read the same structured intelligence agents get — no code.
{% endtab %}
{% endtabs %}

## Service availability by channel

| Service | x402 | OpenClaw skill | Virtuals ACP | Browser |
| --- | :---: | :---: | :---: | :---: |
| Quick scan — $0.02 | ✅ | ✅ | ✅ | ✅ |
| Market intel — $0.20 | ✅ | ✅ | ✅ | ✅ |
| Deep dive — $0.50 | ✅ | ✅ | ✅ | ✅ |
| Trade / BYOW swap — $0.15 | ✅ | ➖ | ✅ | ➖ |

✅ available · ➖ not in this channel yet

{% hint style="warning" %}
The **OpenClaw skill (v1)** and the **browser** currently expose the three scanners only. The two-phase BYOW [trade](../api-reference/trade.md) flow is available via x402 and Virtuals ACP.
{% endhint %}

## Price & data parity

No path is cheaper or richer than another. A quick scan is $0.02 whether it's hit from a raw HTTP call, an OpenClaw agent, ACP escrow, or the browser — and the response schema is the same `schema_version: "2.0"` shape everywhere.
