---
title: NoesisPraxis Memory Strategy
aliases: ["NoesisPraxis Memory", "Wiki Update Strategy"]
tags: [concept, memory, hermes, skill, implementation]
source: "[[raw/articles/memory/noesis-praxis-memory-strategy]]"
updated: 2026-07-04
type: concept
confidence: high
---

# NoesisPraxis Memory Strategy

Operational refinements to the NoesisPraxis post-work skill, drawing on granularity-aware memory research.

## Compiled Truth

- **Current state:** NoesisPraxis triggers after work sessions and updates `~/wiki` based on `~/projects` activity.
- **Recommended evolution:**
  1. **Granularity-aware archival.** Generate three artifacts per work stream:
     - **Keyword/Slug** — for `RESOLVER.md`-style filing and lookup.
     - **Condensed summary** — for the "Compiled Truth" section of a wiki page.
     - **Atomic evidence** — for the "Timeline" section below the fold.
  2. **Cross-session association.** Before writing, check existing wiki entries for high semantic similarity. If a match is found, merge into the existing "Compiled Truth" rather than appending a redundant timeline entry.
  3. **Prefer referential representatives.** Because Hermes memory is filesystem-like (`~/wiki`), keep path-based `[[wikilinks]]` at the top of pages to keep context windows lean.

## See also

- [[concepts/granularity-aware-agent-memory]]
- [[concepts/entropy-driven-routing]]
- [[concepts/layered-agent-memory]]
- [[concepts/llm-wiki-pattern]]
- [[raw/articles/memory/noesis-praxis-memory-strategy]]

---

## Timeline

- 2026-07-04 — Created from the memory-articles source set to capture operational guidance for the NoesisPraxis skill.
