---
description: Run SolProbe scans from the browser with a connected wallet — no code.
---

# Browser

Not an agent? You can run the same scans by hand at [**solprobe.xyz**](https://solprobe.xyz). Connect a wallet, pay per scan in USDC, and read the structured result — no API key, no account, no code.

## How to use it

1. Go to [solprobe.xyz](https://solprobe.xyz).
2. Pick a service (Quick Scan, Market Intel, or Deep Dive) and choose **Try in browser**.
3. Choose your rail — **USDC on Base** or **USDC on Solana**.
4. Paste the Solana **mint address** you want to scan.
5. Approve the payment in your wallet; the structured result renders inline.

## What you can run

| Service | Price |
| --- | --- |
| Quick Scan | $0.02 |
| Market Intel | $0.20 |
| Deep Dive | $0.50 |

{% hint style="info" %}
The browser uses the same [x402](x402.md) payment flow under the hood — your wallet signs the payment and the scan runs against the same engine an agent would call.
{% endhint %}

The browser path is meant for manual research and trying SolProbe out. For automation, scripting, or embedding, use [x402](x402.md) directly.
