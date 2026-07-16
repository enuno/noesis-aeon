# Brain Wiki AGENTS

Canonical conventions for the root wiki at /home/elvis/wiki.

## Authority
- AGENTS.md is the source of truth for the root wiki.
- SCHEMA.md is a compatibility alias for legacy references.
- RESOLVER.md is the filing decision tree; consult it before creating or renaming pages.
- If a directory has its own AGENTS.md, follow that file for work in that subtree.
- Root rules still apply unless a scoped file adds stricter guidance that does not conflict with root provenance or immutability rules.

## Session orientation
Before touching existing wiki content in a new session:
1. Read AGENTS.md.
2. Read SCHEMA.md only for legacy format notes.
3. Read RESOLVER.md.
4. Read index.md.
5. Read the recent log.md entries.
6. Search for existing pages before creating anything new.

## Filing model
Use RESOLVER.md to choose the destination. Current top-level destinations:
- people/
- companies/
- deals/
- meetings/
- projects/
- ideas/
- concepts/
- writing/
- programs/
- org/
- civic/
- media/
- personal/
- household/
- hiring/
- sources/
- prompts/
- inbox/
- archive/

Heuristics:
- human being -> people/
- organization -> companies/
- active build with repo/spec/team -> projects/
- reusable framework or mental model -> concepts/
- prose artifact -> writing/
- raw import or archived snapshot -> sources/
- historical or dead material -> archive/
- unsure -> inbox/

## Page conventions
- Use lowercase hyphenated filenames.
- Prefer updating an existing page over creating a duplicate.
- Keep titles, aliases, tags, sources, and updated timestamps consistent with nearby pages.
- Use only tags already defined by the wiki taxonomy.
- Keep pages scannable; split long pages into hub + subpages.
- Do not create placeholders like temp, draft, untitled, or final.
- Preserve historical claims when they matter; do not silently collapse conflicts.

## Source handling
- Files under sources/ are immutable after ingest.
- Corrections belong in wiki pages, not in source files.
- When source-backed claims conflict, keep both positions visible and label the uncertainty.
- For legal or civic material, keep provenance explicit and avoid replacing evidence with conclusions.
- If your wiki uses a different raw folder name (e.g., `raw/`), the same immutability rule applies: write new versions to a new path rather than overwriting the ingested source.

## Update flow
1. Check index.md and search existing pages before creating or renaming anything.
2. Make the smallest coherent edit set.
3. Update linked pages and index.md in the same pass.
4. Update log.md in the same pass.
5. If a claim changes, note the reason in the page and log.

## Verification
- Broken wikilinks
- Orphan pages
- Index completeness
- Source drift
- Stale or contradictory content
- Markdown hygiene with git diff --check
- Working tree clean or intentionally scoped

## Log format
```markdown
## YYYY-MM-DD: <Action> | <Short Title>

- <bullet per file created or updated>
- Source: `sources/path.md` (if applicable)
- Method: <workflow or trigger used>
```

Log entries go at the bottom of log.md.

## Compatibility note
SCHEMA.md mirrors this file for legacy references. When conventions differ, AGENTS.md wins.
