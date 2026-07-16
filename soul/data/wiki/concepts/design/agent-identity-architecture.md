---
title: Canonical Architecture for Agent-Bound ERC-8004 Tokens
created: 2026-07-16
updated: 2026-07-16
type: concept
tags: ["architecture", "erc-8004", "ai-agents", "identity", "nft", "design", "smart-contracts"]
confidence: high
sources: ["sources/agent-standards/eip-8004-trustless-agents.md", "sources/agent-standards/eip-8217-agent-nft-identity-bindings.md"]
---

## Summary

This is the internal reference architecture for TerraHash/Ryno/ServerDomes agent identities. It separates identity (a non-transferable ERC-8004 token), reputation (on-chain feedback + off-chain scoring), validation (capability attestations), and control (an external controller NFT via ERC-8217). The design is proxy-ready, modular, and keeps economics out of the identity layer.

## Core Components

### 1. Identity Contract (ERC-8004 Registry)

- ERC-721 implementation with URIStorage.
- One `agentId` per agent. Invariants: 1:1 mapping from agentId to tokenId; transfer disabled if soulbound policy is active.
- Minting role restricted to factory/admin.
- Burn only by admin or via a decommission proposal.
- Metadata keys: `agentWallet`, `agent-binding`, `agent-collection`, `capabilities`.

### 2. Reputation Contract

- Data structures: per-agent feedback array (value, decimals, tag1, tag2, revoked), per-client index, summary cache.
- Writers: any non-owner address (client). Optional: allow only whitelisted reviewers or stake-gated reviewers.
- Query interfaces: filtered summaries by agent, reviewer set, and tags.
- Off-chain indexers compute weighted scores and publish periodic attestations back to the Validation Registry.

### 3. Validation / Capabilities Contract

- Records validation requests and responses for test suites, benchmarks, and security checks.
- Capability flags: bitfield or string tags (e.g., `btc-treasury`, `hashrate-optimization`, `edge-network`).
- Off-chain validators run deterministic tests and call `validationResponse` with `response` and evidence URI.
- Examples: ERC-8126 verification provider, custom TerraHash test harnesses, TEE attestation.

### 4. Composition with ERC-8041 / ERC-8217 / ERC-8263 / OCP

- Use ERC-8041 for numbered fleet collections.
- Use ERC-8217 to bind each agent to a controller NFT.
- Use ERC-8263 + OCP to anchor observations and decisions from the agent runtime.
- Keep ERC-20 / governance tokens separate; they reference the agent identity but do not define it.

## Invariants

- Identity is durable: reputation and validation history must survive registry upgrades.
- Reputation is non-transferable: scores do not move with a token sale.
- Control is separable: ownership of the controller NFT does not alter the agent's historical record.
- Economics are external: payments, revenue shares, and rights use ERC-20 or separate contracts.

## Pseudocode: Registry Factory

```solidity
contract TerraHashAgentRegistry is ERC721URIStorage, Ownable2Step {
  mapping(uint256 => bytes) internal _metadata;
  uint256 public totalAgents;
  bool public soulbound;

  function registerAgent(string calldata uri, address controller) external onlyMinter returns (uint256 agentId) {
    agentId = ++totalAgents;
    _safeMint(controller, agentId);
    _setTokenURI(agentId, uri);
    emit Registered(agentId, uri, controller);
  }

  function _beforeTokenTransfer(address from, address to, uint256 tokenId, uint256 batchSize) internal override {
    require(!soulbound || from == address(0), "soulbound");
    super._beforeTokenTransfer(from, to, tokenId, batchSize);
  }
}
```

## Implementation Checklist

- [ ] Decide soulbound vs transferable for identity tokens.
- [ ] Split identity, reputation, validation, and economics into separate contracts.
- [ ] Use ERC-8217 bindings to external controller NFTs for ownership separation.
- [ ] Reserve metadata keys and restrict writes to authorized contracts.
- [ ] Define capability tags and validation test suites per agent class.
- [ ] Document registry upgrade path that preserves tokenIds and history.
