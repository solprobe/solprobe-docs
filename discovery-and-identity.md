---
description: Machine-readable discovery surfaces and on-chain agent identity.
---

# Discovery & identity

SolProbe is built to be **found and verified by other agents**. It publishes standard discovery documents and carries an on-chain agent identity on both Base and Solana.

## Discovery surfaces

All free and unpaywalled, served from `https://api.solprobe.xyz`:

| Surface | Path | What it is |
| --- | --- | --- |
| x402 manifest | `/.well-known/x402` | Endpoint discovery — lists every payable route |
| OpenAPI 3.1 | `/openapi.json` | Canonical spec: routes, request/response schemas, per-endpoint pricing (`x-payment-info`), and agent guidance |
| LLM doc | `/llm.txt` | Plain-text response schemas for LLM agents to read directly |
| Agent card (A2A) | `/.well-known/agent.json` | Agent identity + skills, A2A format |
| Agent registration | `/.well-known/agent-registration.json` | ERC-8004 registration file pointed at by the on-chain identity NFTs |

{% hint style="info" %}
`/openapi.json` is **canonical** for endpoints + pricing; `/.well-known/x402` is the strict v1 fan-out (route list only). Agents typically fan out from the manifest to the OpenAPI spec or the live `402` challenge.
{% endhint %}

## On-chain identity (ERC-8004)

SolProbe is registered as an agent on both chains, so its identity and services are independently verifiable:

| Chain | Identity |
| --- | --- |
| Base | agentId `51645` on IdentityRegistry `0x8004A169FB4a3325136EB29fA0ceB6D2e539a432` |
| Solana | asset `2kYR36PKrxA7Gh8Po3Y4dJAhYDk2nCYVjFmjtJDoNNj7` on the 8004-solana AgentRegistry |

## Indexers

SolProbe's x402 resources are indexed publicly:

- **x402scan:** [server profile](https://www.x402scan.com/server/3cd1b555-1593-44d7-8fa5-0c24b0e14899) — both Base and Solana payment rails listed.

## Links

- Website: [solprobe.xyz](https://solprobe.xyz)
- OpenClaw skill: [github.com/solprobe/solprobe-skills](https://github.com/solprobe/solprobe-skills)
- X / Twitter: [@solprobe](https://x.com/solprobe)
