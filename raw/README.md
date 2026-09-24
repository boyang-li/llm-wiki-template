---
type: raw-source-guide
status: active
updated: <YYYY-MM-DD>
---

# Raw Sources

This folder stores curated source material for this wiki.

Sources are the source of truth. The LLM may read and summarize them, but should not rewrite them during normal wiki maintenance.

## Suggested organization

- `articles/` - clipped web articles and long-form references.
- `docs/` - project docs, design docs, requirements, implementation notes.
- `meetings/` - meeting transcripts, notes, decisions, action items.
- `tickets/` - ticket exports, issue summaries, incident records.
- `assets/` - images, diagrams, screenshots, PDFs, whiteboards, exports.

Create subfolders as the corpus grows. Keep file names descriptive and date-prefixed when useful, for example `2026-06-22-project-name-design.md`.

## Ingestion notes

When adding a source, try to preserve:

- Original title.
- Date or approximate date.
- Author, team, or source system when available.
- Links to related assets.
- Any confidentiality or handling notes.
