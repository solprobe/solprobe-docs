---
description: Two-phase, bring-your-own-wallet Solana swap — free quote, paid execute.
---

# Trade (BYOW)

A **Mode A bring-your-own-wallet** swap executor on top of Jupiter routing, with a built-in risk gate. SolProbe never holds your keys: you get an unsigned transaction, sign it locally, and post it back for broadcast. The fee is charged **only on commit**.

{% hint style="info" %}
Available via [x402](../access-paths/x402.md) and [Virtuals ACP](../access-paths/virtuals-acp.md). Not in the v1 OpenClaw skill or the browser.
{% endhint %}

## Two-phase flow

```
1. POST /trade/quote     (free)   → unsigned Solana tx + risk gate
2. sign the tx locally   (your wallet, your keys)
3. POST /trade/execute   ($0.15)  → broadcasts, returns the tx signature
```

The $0.15 fee settles **only when a trade actually CONFIRMs**. A non-confirmed execute returns HTTP `422` over x402 and the payment is cancelled — you're not charged for a trade that didn't happen.

## `POST /trade/quote` — free

Returns an unsigned swap transaction and the risk-gate result. (Generate or pass a `job_id`; the quote response carries the `unsigned_transaction_b64` to sign.)

## `POST /trade/execute` — $0.15 on commit

```json
{
  "job_id": "direct_1700000000_abc123",
  "signed_transaction_b64": "<base64 signed Solana tx>"
}
```

| Response field | Type | Description |
| --- | --- | --- |
| `status` | enum | `CONFIRMED`, `FAILED`, or a `REJECTED_*` reason (validation, risk gate, balance, route, price impact, slippage, …) |
| `execution` | object \| null | `{ tx_signature, slot }` on success |
| `rejection` | object \| null | `{ code, reason, refundable }` when not confirmed |

Plus `schema_version: "2.0"`.

## Helper routes (free)

| Endpoint | Purpose |
| --- | --- |
| `GET /trade/status/:job_id` | Poll a job's status |
| `GET /trade/pairs` | Verified tradeable tokens (mint, symbol, decimals) |
| `GET /trade/currencies` | Accepted payment currencies + chain |

{% hint style="warning" %}
Always run a [Quick scan](quick-scan.md) before trading — the risk gate screens obvious hazards, but the structural grade is your first line of defense.
{% endhint %}
