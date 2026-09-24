# LLM Wiki Operating Guide

This vault is an LLM-maintained personal or team wiki: a persistent, compounding knowledge base built from curated raw sources. See [[llm-wiki]] for the high-level idea behind this pattern.

The human curates raw sources and asks questions. The LLM maintains the wiki layer: summaries, cross-references, synthesis, index updates, and the chronological log.

> This file is a starting template. Rename the placeholder scope below, and adapt directory names, workflows, and conventions to fit your domain as you and the LLM co-evolve this document.

**Scope:** `<describe what this wiki is about — e.g. a company, a research topic, a book, a personal knowledge base>`

## Core principles

- Treat `raw/` as immutable source material. Read it, cite it, and summarize it, but do not modify source files except to organize newly added files when explicitly asked.
- Treat `wiki/` as the maintained knowledge layer. Create and update pages there whenever sources are ingested or questions produce reusable knowledge.
- Keep [index.md](index.md) content-oriented and current. It is the first place to look before answering questions or updating wiki pages.
- Keep [log.md](log.md) chronological and append-only. Every ingest, major query, lint pass, and structural maintenance pass gets a dated entry.
- Prefer explicit uncertainty over invented certainty. Mark unclear claims as `Needs verification` and point to the source or missing evidence.
- Preserve confidentiality. Do not send sensitive or private content to external services unless the user explicitly approves that workflow.

## Directory structure

- `raw/` - curated source material, grouped by source type or domain.
- `raw/assets/` - locally stored images, diagrams, screenshots, exports, PDFs, and other attachments referenced by sources.
- `wiki/` - LLM-generated and LLM-maintained markdown knowledge pages.
- `wiki/sources/` - one summary page per ingested source or source bundle.
- `wiki/projects/` - project pages, roadmaps, milestones, risks, design history.
- `wiki/systems/` - systems, applications, services, platforms, integrations, and how they relate.
- `wiki/decisions/` - ADR-style decisions and tradeoff records.
- `wiki/concepts/` - domain concepts, terminology, patterns.
- `wiki/people-teams/` - people, teams, roles, responsibilities, ownership notes. Avoid private personal details unless relevant.
- `wiki/meetings/` - meeting summaries and extracted action/decision records.
- `wiki/questions/` - durable answers, investigations, comparisons, and analysis generated from user queries.
- `wiki/diagrams/` - diagram notes, Mermaid diagrams, image inventories, and explanation pages.
- `wiki/runbooks/` - operational procedures, repeatable workflows, verification steps, and administration notes synthesized from raw sources.
- `templates/` - reusable markdown templates for consistent wiki pages.

Add, rename, or remove `wiki/` subfolders as your domain requires (for example, `wiki/characters/` and `wiki/themes/` for reading a book, or `wiki/data/` for a data-asset-heavy wiki). Document any structural change here and in [log.md](log.md).

## Ingest workflow

When the user adds a new raw source and asks for ingestion:

1. Identify the source path, type, date, author/team if available, and topic.
2. Read the source and any referenced local assets that are needed for comprehension.
3. Create or update a page in `wiki/sources/` summarizing the source.
4. Update affected pages under `wiki/projects/`, `wiki/systems/`, `wiki/decisions/`, `wiki/concepts/`, `wiki/people-teams/`, `wiki/meetings/`, `wiki/questions/`, or `wiki/diagrams/`.
5. Add links between pages using Obsidian-style wiki links, for example `[[wiki/systems/Example System]]`.
6. Update [index.md](index.md) with new or changed pages.
7. Append a dated entry to [log.md](log.md) using the standard heading format.

For the first 10-20 ingests, propose the affected page list before editing many pages, so the human can tune what counts as important for this wiki.

## Query workflow

When answering a question:

1. Read [index.md](index.md) first to identify likely relevant pages.
2. Read the relevant wiki pages and, only when needed, the underlying raw sources.
3. Answer with citations to wiki pages or raw source paths.
4. If the answer is reusable, offer to file it under `wiki/questions/` or create it directly if the user asked for wiki maintenance.
5. Update [index.md](index.md) and [log.md](log.md) if a durable page is created or materially updated.

## Lint workflow

Periodically run a wiki health check:

- Find orphan pages with no inbound links.
- Find pages mentioned in text but not created yet.
- Find stale claims that conflict with newer sources.
- Find important systems, projects, decisions, or concepts that lack a page.
- Find diagrams or image assets that are referenced but not explained.
- Check whether [index.md](index.md) accurately represents the current wiki.
- Append findings and maintenance actions to [log.md](log.md).

## Page conventions

- Use concise YAML frontmatter on generated pages when useful.
- Include `status`, `created`, `updated`, `source_count`, and `confidence` when applicable.
- Put the most important current synthesis near the top.
- Maintain a `Sources` section with links to raw files or `wiki/sources/` pages.
- Maintain `Related` links so Obsidian graph view stays useful.
- Prefer Mermaid for diagrams that can be represented as text. Use local image files for screenshots, architecture diagrams, whiteboards, and exported diagrams.
- Mermaid compatibility caveat: diagrams must render in VS Code as well as Obsidian. Use the stricter `graph LR` / `graph TD` syntax instead of `flowchart`, quote labels that contain spaces, slashes, punctuation, or colons, use `<br/>` instead of raw `\n` line breaks, split long chained edges into simple edge statements, and avoid labeled dotted-edge syntax such as `-. label .->`.

## Standard log heading

Use this exact heading shape so the log remains searchable:

```markdown
## [YYYY-MM-DD] type | Short title
```

Recommended `type` values: `setup`, `ingest`, `query`, `lint`, `maintenance`, `decision`.
