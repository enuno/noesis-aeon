---
title: Operational Playbook: Agent Identity Lifecycle and Security
created: 2026-07-16
updated: 2026-07-16
type: concept
tags: ["operations", "erc-8004", "ai-agents", "security", "lifecycle", "policy"]
confidence: high
sources: ["sources/agent-standards/eip-8004-trustless-agents.md", "sources/agent-standards/eip-8217-agent-nft-identity-bindings.md"]
---

## Summary

This playbook covers the full lifecycle of an agent identity in production: creation, key rotation, controller transfer, decommission, and abuse prevention. It assumes a soulbound identity NFT bound to a transferable controller NFT via ERC-8217, with reputation and validation stored on-chain.

## Lifecycle

### 1. Agent Creation

1. Deploy or select controller NFT (project, character, governance NFT).
2. Call registry `register(agentURI, metadata)` to mint agent identity.
3. Set `agent-binding` metadata to the canonical binding contract.
4. Set `agentWallet` via EIP-712 signature for the agent's operational key.
5. Publish registration JSON to IPFS or HTTPS with `.well-known/agent-registration.json`.
6. Register initial capabilities and run validation suite.

### 2. Key Rotation

- Rotate the `agentWallet` by signing a new EIP-712 message from the current wallet or controller owner.
- The agent NFT and history do not change; only the operational key updates.
- Log the rotation event on-chain and in off-chain audit logs.

### 3. Controller Transfer

- Transfer the controller NFT; the agent identity stays bound.
- Clear `agentWallet` after transfer so the new controller must re-verify it.
- Reputation remains with the agent, not the old controller.

### 4. Decommission

- Mark agent `active: false` in registration JSON.
- Optionally burn the identity token after a cooldown.
- Archive validation evidence and observation commitments.
- Keep reputation/validation history immutable for audit.

## Security and Abuse Prevention

**Preventing reputation sale**

- Make identity tokens non-transferable (soulbound). Reputation is attached to the agent, not sellable.
- If transfer is required, clear reputation summary and force re-validation.

**Sybil mitigation**

- Mint costs or stake requirements.
- Whitelist reviewers for internal feedback.
- Cap feedback per reviewer per time window.
- Cross-reference agent wallets and controller NFTs.

**Monitoring**

| Event | Signal | Action |
|---|---|---|
| `Registered` | New agent | Verify metadata and initial validation |
| `AgentWallet` changed | Key rotation | Confirm signature, update runtime config |
| `AgentBound` | Controller set | Record controller NFT and standard |
| `ValidationResponse` | New attestation | Update capability cache |
| `NewFeedback` | Reputation change | Recompute off-chain score |
| `AnchorProof` | Observation committed | Index for audit trail |

## Policy Templates

- `policy:treasury`: only agents with `capability:treasury` and `reputation-score >= 80` may propose trades.
- `policy:edge-ops`: only agents with `capability:edge-network` and validation tag `thermal-safety:pass` may issue HVAC commands.
- `policy:validator-governance`: only validators on the `TH_VALIDATOR_ALLOWLIST` may submit `validationResponse`.

## Implementation Checklist

- [ ] Document the creation, rotation, transfer, and decommission procedures.
- [ ] Enforce soulbound identity if reputation must not be sold.
- [ ] Automate `.well-known` domain verification at registration.
- [ ] Set up event monitoring for registry, validation, and proof anchors.
- [ ] Define policy thresholds per agent class and capability.
- [ ] Run periodic sybil and anomaly reviews on reviewer sets.
