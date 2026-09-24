# llm-wiki-template
This repo serves as a scaffold for a llm wiki knowledge base built with agentic AI+Obsidian (inspired by Andrej Karpathy's llm-wiki gist)

## Getting started

1. Open this repo as an Obsidian vault.
2. Read [llm-wiki.md](llm-wiki.md) for the underlying idea.
3. Read [AGENTS.md](AGENTS.md) — the operating guide your LLM agent follows. Fill in the `<scope>` placeholder for your domain.
4. Read [How to Use This Wiki.md](How%20to%20Use%20This%20Wiki.md) for a practical first-week plan.
5. Start dropping sources into `raw/`, track them in `raw/source-inventory.md`, and ask your agent to ingest them.

## Structure

- `raw/` - immutable curated source material (`articles/`, `docs/`, `meetings/`, `tickets/`, `assets/`).
- `wiki/` - LLM-maintained knowledge pages (`sources/`, `projects/`, `systems/`, `decisions/`, `concepts/`, `people-teams/`, `meetings/`, `questions/`, `diagrams/`, `runbooks/`).
- `templates/` - reusable page templates for sources, projects, systems, decisions, and meetings.
- `index.md` - content-oriented navigation catalog.
- `log.md` - append-only chronological activity log.
