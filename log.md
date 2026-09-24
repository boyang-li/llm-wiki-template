---
type: log
status: active
created: <YYYY-MM-DD>
---

# Wiki Log

Append-only chronological record of ingests, queries, lint passes, and maintenance.

Use this heading format for every entry:

```markdown
## [YYYY-MM-DD] type | Short title
```

Recommended `type` values: `setup`, `ingest`, `query`, `lint`, `maintenance`, `decision`.

## [<YYYY-MM-DD>] setup | Initial vault scaffold

Created the initial LLM-maintained wiki scaffold based on the LLM Wiki playbook.

Files and folders initialized:

- `llm-wiki.md` the underlying idea behind this wiki pattern.
- `AGENTS.md` operating guide for future LLM agents.
- `How to Use This Wiki.md` practical getting-started guide.
- `Welcome.md` vault entry point.
- `index.md` content-oriented navigation catalog.
- `log.md` chronological activity log.
- `raw/` immutable source layer.
- `raw/assets/` local asset storage for images, diagrams, screenshots, PDFs, and attachments.
- `raw/articles/`, `raw/docs/`, `raw/meetings/`, and `raw/tickets/` source categories.
- `wiki/` generated knowledge layer.
- `wiki/sources/`, `wiki/projects/`, `wiki/systems/`, `wiki/decisions/`, `wiki/concepts/`, `wiki/people-teams/`, `wiki/meetings/`, `wiki/questions/`, `wiki/diagrams/`, and `wiki/runbooks/` knowledge categories.
- `templates/` reusable page templates.

No source material has been ingested yet.
