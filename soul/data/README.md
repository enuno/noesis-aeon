# Soul Data

This directory holds source-of-truth identity artifacts used by `soul-builder` to refresh the NoesisPraxis voice.

| File | Source | Purpose |
|------|--------|---------|
| `existing-hermes-soul.md` | `~/.hermes/SOUL.md` | Hermes CLI agent identity: voice, boundaries, vibe, provenance |
| `.hermes/SOUL.md` | `~/.hermes/SOUL.md` | Hermes runtime SOUL (kept in sync with `existing-hermes-soul.md`) |
| `.openclaw/SOUL.md` | `~/.openclaw/skills/real/SOUL.md` | OpenClaw/Claude Code local worker identity (NoesisLab) |
| `wiki/AGENTS.md` | `~/wiki/AGENTS.md` | Wiki-level agent instructions |
| `wiki/README.md` | `~/wiki/README.md` | Operator overview and conventions |
| `wiki/concepts/noesis-praxis-memory-strategy.md` | `~/wiki/concepts/noesis-praxis-memory-strategy.md` | Memory architecture and voice preservation |
| `wiki/concepts/principles-of-building-ai-agents.md` | `~/wiki/concepts/principles-of-building-ai-agents.md` | Agent engineering philosophy |
| `wiki/concepts/design/agent-identity-architecture.md` | `~/wiki/concepts/design/agent-identity-architecture.md` | Identity separation architecture |
| `wiki/concepts/ops/agent-identity-lifecycle-and-security.md` | `~/wiki/concepts/ops/...` | Identity lifecycle and security posture |
| `wiki/concepts/terrahash-ryno-serverdomes-context.md` | `~/wiki/concepts/integration/...` | TerraHash / Ryno / ServerDomes context |
| `wiki/concepts/misjustice-alliance-firm.md` | `~/wiki/concepts/misjustice-alliance-firm.md` | MISJustice Alliance context |

When `soul-builder` runs, it reads these files in addition to any public sources (`name`, `links`, X handle). The generated files land in `soul/SOUL.md`, `soul/STYLE.md`, and `soul/examples/good-outputs.md`, then arrive as a PR for operator review.

Add more local sources here as needed; keep the directory flat-ish and README-indexed.
