---
title: TerraHash / Ryno / ServerDomes Integration Context
created: 2026-07-16
updated: 2026-07-16
type: concept
tags: ["integration", "terrahash", "ryno", "serverdomes", "bitcoin-mining", "treasury", "edge", "ai-agents"]
confidence: high
sources: ["sources/agent-standards/eip-8004-trustless-agents.md", "concepts/standards/erc-8263-and-ocp.md"]
---

## Summary

This page maps the ERC-8004 agent identity stack to the TerraHash / Ryno Crypto Mining / ServerDomes operating environment. The same identity layer can serve mining optimization agents, treasury agents, and edge datacenter operations agents, with capability tags and validation suites specific to each domain.

## Agent Classes

### Bitcoin Mining Optimization Agents

- Identity: one ERC-8004 agent per fleet or per mining site.
- Capabilities: `hashrate-optimization`, `energy-curtailment`, `asic-health`, `pool-routing`.
- Validations: thermal-safety test, power-limit test, profit-backtest, MCP server health check.
- Observations: anchor hashrate decisions, energy bids, and tuning events via ERC-8263/OCP.
- Controller: farm ownership NFT or a ServerDomes fleet NFT.

### Treasury and DeFi Strategy Agents

- Identity: one agent per strategy or vault.
- Capabilities: `btc-treasury`, `stablecoin-yield`, `hedge-execution`, `derivatives`.
- Validations: backtest pass, risk-limit test, multisig co-signer attestation, ERC-8126 security scan.
- Observations: anchor trade intent, execution parameters, and risk checks via ERC-8263/OCP.
- Controller: treasury governance NFT or multisig.

### Edge / IoT / Datacenter Operations Agents

- Identity: one agent per ServerDomes edge site or major subsystem.
- Capabilities: `edge-network`, `hvac-control`, `power-distribution`, `predictive-maintenance`.
- Validations: physical access attestation, TEE oracle, safety interlock test, network reachability.
- Observations: anchor control commands and sensor readings via ERC-8263/OCP.
- Controller: site NFT or facility governance token.

## Cross-Cutting Policies

| Policy | Rule |
|---|---|
| `TH_POLICY_MIN_REPUTATION` | reputation-score >= 75 for autonomous actions |
| `TH_POLICY_VALIDATION_WINDOW` | validation must be within 30 days |
| `TH_POLICY_ANCHOR_CRITICAL` | all spend/physical-control actions anchored via ERC-8263 |
| `TH_POLICY_CONTROLLER_VERIFY` | runtime verifies controller NFT ownership before acting |
| `TH_POLICY_KEY_ROTATION` | agentWallet must rotate every 90 days |

## Recommended Chain Deployment

- Base mainnet for identity registry, validation registry, and ERC-8263 anchors. Low fees, good tooling, aligned with existing x402 stack.
- Ethereum mainnet for high-stakes treasury identities if stronger settlement guarantees are needed.
- Use the same `agentWallet` derivation across chains; identity resolution can be per-chain via ERC-8004 registries.

## Ecosystem Alignment

- This layer complements existing TerraHash MCP servers (Bitmain, Braiins, ESP-Miner, Luxor).
- It also complements the `[[terrahash-x402]]` paid gateway: agents can advertise services via ERC-8004 registration and settle per-request via x402.

## Implementation Checklist

- [ ] Define agent classes and capability tags for mining, treasury, and edge ops.
- [ ] Design validation suites for each class with deterministic pass/fail criteria.
- [ ] Choose chain deployment and registry ownership model.
- [ ] Integrate ERC-8263 anchoring into agent action loops.
- [ ] Wire orchestrators to filter and route by on-chain identity and trust.
- [ ] Align with x402 payment rails and existing MCP servers.
