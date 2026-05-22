---
description: Fund a wallet, make your first SolProbe call, and read the response.
---

# Getting started

You can be scanning tokens in a couple of minutes. There's **no key, no account, and no signup** — payment and identity ride on your wallet via [x402](access-paths/x402.md).

## 1. Fund a wallet

SolProbe charges per call in **USDC**, on either rail (same price):

| Network | Chain ID (CAIP-2) | USDC asset |
| --- | --- | --- |
| Base | `eip155:8453` | `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` |
| Solana | `solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp` | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` |

{% hint style="info" %}
On Base, settlement is **gasless** — you sign an EIP-3009 permit and the x402 facilitator pays gas. Your wallet only needs USDC, not ETH.
{% endhint %}

## 2. Pick how you'll call it

| You are… | Use |
| --- | --- |
| An agent or app calling HTTP directly | [x402](access-paths/x402.md) |
| Running on OpenClaw | [OpenClaw skill](access-paths/openclaw-skill.md) |
| In the Virtuals ecosystem | [Virtuals ACP](access-paths/virtuals-acp.md) |
| A human doing manual research | [Browser](access-paths/browser.md) |

Not sure? See [**Access paths → Overview**](access-paths/README.md).

## 3. Make your first call

The fastest path for an agent is an x402-aware HTTP client that handles the `402 → sign → retry` handshake for you.

{% tabs %}
{% tab title="TypeScript (@x402/fetch)" %}
```typescript
import { x402Client, wrapFetchWithPayment } from "@x402/fetch";
import { registerExactEvmScheme } from "@x402/evm/exact/client";
import { privateKeyToAccount } from "viem/accounts";

const signer = privateKeyToAccount(process.env.BUYER_PRIVATE_KEY as `0x${string}`);
const client = new x402Client();
registerExactEvmScheme(client, { signer });           // pay on Base
const paidFetch = wrapFetchWithPayment(fetch, client); // handles 402 automatically

const res = await paidFetch("https://api.solprobe.xyz/scan/quick", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ token_address: "DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263" }),
});

console.log(await res.json()); // { schema_version: "2.0", structural_risk_grade: "A", ... }
```
{% endtab %}

{% tab title="curl (see the 402)" %}
```bash
# Without payment you get the 402 challenge (this is the discovery step):
curl -i -X POST https://api.solprobe.xyz/scan/quick \
  -H "Content-Type: application/json" \
  -d '{"token_address":"DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263"}'
# → HTTP/1.1 402 Payment Required   (accepts[] lists Base + Solana options)
```
Signing the payment by hand is involved — use an x402 client library for the full round trip. See the [Payment guide](payment-guide.md).
{% endtab %}
{% endtabs %}

## 4. Read the response

Every response is JSON and always includes these envelope fields:

| Field | Meaning |
| --- | --- |
| `schema_version` | Always `"2.0"` |
| `data_confidence` | `HIGH` · `MEDIUM` · `LOW` — confidence in the verdict |
| `data_quality` | `FULL` · `PARTIAL` · `LIMITED` — how complete the source data was |
| `missing_fields` | Any inputs that couldn't be fetched |

{% hint style="success" %}
SolProbe **never returns a hard error to a caller** — it degrades gracefully and tells you, via `data_quality` and `missing_fields`, how much to trust the result.
{% endhint %}

Next: full request/response shapes in the [API reference](api-reference/README.md).
