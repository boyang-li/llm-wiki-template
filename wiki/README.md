---
type: wiki-guide
status: active
updated: <YYYY-MM-DD>
---

# Wiki Layer

This folder contains the LLM-generated and LLM-maintained knowledge layer for this wiki.

The wiki should become the current, navigable synthesis of the raw source corpus. It is expected to change as new sources are added.

## Subfolders

- `sources/` - summaries of ingested raw sources.
- `projects/` - project and initiative pages.
- `systems/` - systems, applications, platforms, integrations, and how they relate.
- `decisions/` - ADR-style decisions and tradeoff records.
- `concepts/` - terminology, domain concepts, patterns.
- `people-teams/` - people, team ownership, responsibilities, and collaboration context.
- `meetings/` - meeting summaries, action items, and extracted decisions.
- `questions/` - durable answers and investigations generated from user queries.
- `diagrams/` - diagram explanations, Mermaid diagrams, and asset inventories.
- `runbooks/` - operational procedures, repeatable workflows, verification steps, and administration notes synthesized from raw sources.

Add or rename subfolders as your domain requires; update this file and [[AGENTS]] when you do.

## Maintenance rule

Whenever a page in this folder is created or materially updated, update [../index.md](../index.md) and append a note to [../log.md](../log.md).
