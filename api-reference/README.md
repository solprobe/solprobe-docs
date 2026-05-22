---
description: Request and response shapes for every SolProbe service.
---

# API reference

All endpoints are `POST` to `https://api.solprobe.xyz`, take a JSON body, and return JSON. Scanner endpoints take a single Solana SPL **mint address**.

| Service | Endpoint | Price | SLA |
| --- | --- | --- | --- |
| [Quick scan](quick-scan.md) | `POST /scan/quick` | $0.02 | < 5s |
| [Market intel](market-intel.md) | `POST /market/intel` | $0.20 | < 10s |
| [Deep dive](deep-dive.md) | `POST /scan/deep` | $0.50 | < 30s |
| [Trade (BYOW)](trade.md) | `POST /trade/quote` → `POST /trade/execute` | free → $0.15 | < 15s |

## Common request field

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `token_address` | string | Yes | Solana SPL mint address — base58, 32–44 chars |

{% hint style="warning" %}
**Solana tokens only.** `token_address` is an SPL mint, not an EVM `0x…` address and not a ticker. Invalid input returns `INVALID_ADDRESS` (HTTP 400).
{% endhint %}

## Response envelope

Every successful response includes:

| Field | Type | Meaning |
| --- | --- | --- |
| `schema_version` | string | Always `"2.0"` |
| `data_confidence` | enum | `HIGH` · `MEDIUM` · `LOW` |
| `data_quality` | enum | `FULL` · `PARTIAL` · `LIMITED` |
| `missing_fields` | string[] | Inputs that couldn't be fetched |
| `confidence` | object | `{ model, data_completeness, signal_consensus }` |

{% hint style="info" %}
SolProbe degrades gracefully and **never returns a hard error to a caller**. If a source is down, it lowers `data_quality`/`data_confidence` and lists `missing_fields` rather than failing.
{% endhint %}

The canonical machine-readable schemas live at [`/openapi.json`](https://api.solprobe.xyz/openapi.json) and [`/llm.txt`](https://api.solprobe.xyz/llm.txt) — if anything here ever disagrees, trust the live endpoint.
