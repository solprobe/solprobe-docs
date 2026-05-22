---
description: How x402 per-call payment works with SolProbe.
---

# Payment guide

SolProbe's paid endpoints use **x402**, an HTTP-native pay-per-use protocol. There's no key or account — your wallet authorizes each call.

## The flow

1. **Request** — your agent `POST`s to a paid endpoint with a JSON body.
2. **402** — the server returns `402 Payment Required` with an `accepts[]` array.
3. **Pay** — your agent signs payment for one `accepts[]` option and retries with an `X-PAYMENT` header.
4. **200** — the facilitator settles the USDC transfer; SolProbe runs the call and returns the result, with a settlement receipt in `X-PAYMENT-RESPONSE`.

An x402 client library (e.g. `@x402/fetch` + `@x402/evm` / `@x402/svm`) performs steps 2–3 automatically. On OpenClaw, the runtime does it for you.

## Networks

Both rails are offered on every paid call, at the **same price** — pick whichever your wallet is funded on:

| Network | Chain ID (CAIP-2) | USDC asset | Notes |
| --- | --- | --- | --- |
| Base | `eip155:8453` | `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` | Gasless — sign an EIP-3009 permit, facilitator pays gas |
| Solana | `solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp` | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` | x402 exact-SVM scheme |

{% hint style="info" %}
The **`payTo` address, amount, and asset come from the live 402 challenge** — read them from `accepts[]` rather than hardcoding. Amounts are atomic (USDC has 6 decimals: `20000` = $0.02).
{% endhint %}

## Reading the 402 challenge

```http
HTTP/1.1 402 Payment Required
```

The challenge body carries `accepts[]`, each entry with:

| Field | Meaning |
| --- | --- |
| `scheme` | `exact` |
| `network` | `eip155:8453` (Base) or `solana:5eykt4…` (Solana) |
| `asset` | USDC contract (Base) / mint (Solana) |
| `maxAmountRequired` | Price in atomic units |
| `payTo` | Address to pay |

## Testing it

```bash
# See the challenge (no charge):
curl -i -X POST https://api.solprobe.xyz/scan/quick \
  -H "Content-Type: application/json" \
  -d '{"token_address":"DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263"}'
# → HTTP/1.1 402 Payment Required
```

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| `402` keeps returning | Confirm the wallet holds enough USDC on the chosen rail, and that the signed payment is in the `X-PAYMENT` header on the retry. |
| `INVALID_ADDRESS` | `token_address` must be a Solana SPL mint (base58, 32–44 chars) — not an EVM `0x…` address or a ticker. |
| `RATE_LIMITED` (429) | Back off and retry; scanner endpoints are rate-limited per IP. |

See also: [x402 protocol](https://x402.org) · SolProbe [discovery surfaces](discovery-and-identity.md).
