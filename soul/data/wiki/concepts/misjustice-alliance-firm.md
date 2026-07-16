---
title: MISJustice Alliance Firm
created: 2026-06-18
updated: 2026-06-20
type: concept
tags: [legal, mcp, architecture, memory, security]
sources:
  - raw/articles/standalone/misjustice-alliance-firm-current-state.md
  - raw/articles/standalone/misjustice-alliance-firm-current-status.md
  - raw/articles/standalone/misjustice-alliance-firm-repo-analysis.md
  - concepts/mindkit-structured-thinking.md
confidence: high
---

# MISJustice Alliance Firm

Current-state concept note for the MISJustice Alliance legal-research platform.

## Executive snapshot

| Property | Value |
|---|---|
| Repository | `~/projects/MISJustice-Alliance/misjustice-alliance-firm` |
| Primary interface | Hermes CLI/TUI |
| Control plane | MCPJungle with RBAC tool groups |
| Shared memory | Honcho |
| Operator boundary | Tailscale-only surfaces |
| Legal retrieval | `legal-corpus` tool group |
| Observability | Prometheus + Grafana |
| Human workflow gates | n8n approval routing |
| Reasoning layer | MindKit structured thinking (repo docs describe this as a proposed Layer 4 sidecar) |

## What the platform is

MISJustice Alliance Firm is a legal research and advocacy platform, not a generic agent playground. The repo describes a system built to:

- centralize agent-facing tool access through MCPJungle
- keep legal, research, technical, and ops tooling separated by policy
- preserve cross-session state through Honcho
- expose dashboards and management UIs only over Tailscale
- keep legal outputs source-backed and human-reviewed before external use

## Current architectural shape

The repo's current architecture story is consistent across `README.md`, `SPEC.md`, `docs/ARCHITECTURE.md`, and the MindKit integration docs:

- Hermes is the primary human-facing interface
- MCPJungle is the control plane and RBAC policy layer
- tool groups include `legal-corpus`, `research`, `technical`, and `all-ops`
- `legal-corpus` routes legal work through Midpage, legal-mcp, American Default MCP, and Congress MCP
- Honcho provides the shared memory substrate
- Prometheus and Grafana provide observability
- n8n is the human-in-the-loop workflow automation layer
- the platform maintains a separate technical/DevOps support stack

## MindKit integration note

The repo also carries a dedicated MindKit architecture and rollout plan.

At the time of this wiki sync, those docs describe MindKit as a proposed Layer 4 reasoning control that sits between an agent's internal reasoning loop and its tool invocation path. The intended shape is:

- internal-only Rust MCP sidecar at `mindkit.internal:3100`
- Tier-2-only prompts
- no public internet egress
- structured trace packets with confidence, assumptions, counterpoints, and warnings
- persistence into Open Notebook and MCAS
- Veritas review for bias, low-confidence, and absolute-statement checks
- staged rollout beginning with Lex, then extending to Rae, Citation, Chronology, Iris, Hermes, and Veritas

The important practical point is that MindKit is documented as an auditable reasoning layer, not a user-facing answer engine.

## Related notes

- [[misjustice-alliance-firm]]
- [[misjustice-alliance-firm/index]]
- [[raw/articles/standalone/misjustice-alliance-firm-current-state]]
- [[raw/articles/standalone/misjustice-alliance-firm-current-status]]
- [[raw/articles/standalone/misjustice-alliance-firm-repo-analysis]]
- [[concepts/mcas-case-management]]
- [[concepts/hitl-governance]]
- [[concepts/memorypalace-agent-memory]]
