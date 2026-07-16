# llm-wiki

Karpathy-style LLM wiki — a private, shared agent knowledge base and authoritative source of truth.

This repository is structured as an Obsidian-compatible markdown vault. It is consumed by both humans and AI agents (RAG, tool context, and long-term memory).

## Stats

- Pages: 1200+
- Chunks: 3607
- Tags: 182

## Structure

```
.
├── index.md                    # Brain index — start here
├── schema.md                   # Page structure and canonical slugs
├── RESOLVER.md                 # Entity resolution rules
├── log.md                      # Vault changelog
├── media/                      # Global image attachments
├── raw/                        # Unprocessed imports and web captures
│   └── assets/                 # Extracted images and PDFs from sources
├── ai-engineer-roadmap/        # 6-phase, 23-week production agent engineering plan
├── ai-research/                # Papers, experiments, findings
├── awp/                        # Agent Work Protocol — wallet, staking, worknets
├── boilerplates/               # Reusable code and config templates
├── build-ai/                   # AI project build notes
├── buildordie/                 # Startup / product build logs
├── concepts/                   # Definitions, architecture decisions, MCP specs
├── hermes/                     # Hermes agent ecosystem documentation
├── langchain/                  # LangChain / LangGraph patterns and logs
├── terrahash-stack/            # TerraHash mining fleet agent stack
├── ywca-missoula/              # Civic / legal accountability documentation
└── ...                         # See index.md for full catalog
```

## Page Conventions

Every page follows the two-layer Brain Schema:

**Above `---`** — Compiled Truth. Current summary, state, open threads, see also.  
**Below `---`** — Timeline. Append-only, reverse-chronological evidence log.

Frontmatter is optional but recommended:

```yaml
---
aliases: ["variant names"]
tags: [tag1, tag2]
source: "url or reference"
updated: YYYY-MM-DD
---
```

### Canonical Slugs

- People: `first-last.md`
- Companies: `company-name.md`
- Disambiguate: `david-liu-crustdata.md`, `david-liu-meta.md`

## Media Policy

- **Images are tracked**: `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`, `.svg`, `.bmp`, `.ico`, `.tiff`
- **PDFs are tracked**: `.pdf`
- **Video and audio are ignored**: `.mp4`, `.mov`, `.mp3`, `.wav`, etc.
- **Large source files are ignored**: `.psd`, `.ai`, `.zip`, `.dmg`, `.iso`, etc.

See `.gitignore` for the full list.

## Tooling

- **Obsidian** — primary editing interface
- **MemPalace** — semantic memory layer (mempalace.yaml auto-generated, do not edit)
- **gbrain** — AI indexing and RAG ingestion

## Contributing

1. Write in markdown. Prefer wikilinks `[[page-name]]` over URLs.
2. Append timeline entries; do not rewrite history below `---`.
3. Keep compiled truth above `---` current and concise.
4. Run `validate-config.mjs` after structural changes.
