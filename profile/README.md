# Sorolens

Real-time monitoring, alerting, and on-chain health checks for Soroban smart contracts on Stellar.

The only observability tool in the Stellar ecosystem with a deployed Soroban watchdog contract for proactive contract monitoring.

## Repositories

| Repo | Description | Stack |
|------|-------------|-------|
| [sorolens](https://github.com/sorolens/sorolens) | Core platform: API, indexer, dashboard, and watchdog contract | Go, Rust, Next.js, Postgres |
| [sorolens-sdk](https://github.com/sorolens/sorolens-sdk) | TypeScript SDK with Zod validation and React hooks | TypeScript, Zod, React |
| [sorolens-cli](https://github.com/sorolens/sorolens-cli) | Command-line interface for querying contract data | Go, Cobra |

## What makes Sorolens different

Existing Stellar observability tools (Stellar Expert, Mercury, StellarChain) are reactive: you look at them after something goes wrong. Sorolens lets contracts report their own health on-chain through a deployed Soroban watchdog contract, making status a first-class, cryptographically-attributable, auditable signal.

## Watchdog contract (testnet)

Contract ID: `CACXRL67WL5KRD6HKWGYADHEUF6RQOCODUN26UQE7MGFZEMIR7PAX6R7`

[View on Stellar Expert](https://stellar.expert/explorer/testnet/contract/CACXRL67WL5KRD6HKWGYADHEUF6RQOCODUN26UQE7MGFZEMIR7PAX6R7) | [View on Stellar Lab](https://lab.stellar.org/r/testnet/contract/CACXRL67WL5KRD6HKWGYADHEUF6RQOCODUN26UQE7MGFZEMIR7PAX6R7)

## Architecture

```
Soroban RPC ──> Indexer ──> Postgres ──> REST API ──> Dashboard
                                                 ──> SDK
                                                 ──> CLI
Watchdog Contract (on-chain)
      │
      ├── ContractRegistered events
      ├── HealthCheckEvent events
      └── ContractAlert events
              │
              └──> Indexer picks up ──> Postgres ──> /api/v1/watchdog/*
```

## Links

- [npm: @sorolens/sdk](https://www.npmjs.com/package/@sorolens/sdk)
- [License: MIT](LICENSE)
