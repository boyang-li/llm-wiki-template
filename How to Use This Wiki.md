---
type: operating-guide
status: active
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

# How to Use This Wiki

This guide explains how to operate this LLM-maintained wiki as a living knowledge base. See [[llm-wiki]] for the underlying idea, and [[AGENTS]] for the operating rules the LLM agent follows.

The goal is not to upload a pile of documents and ask questions against them. The goal is to gradually compile knowledge into a maintained, linked wiki that stays current as new source material arrives.

## The operating model

Keep the three layers separate:

- `raw/` stores original source files and extracted source material.
- `wiki/` stores LLM-maintained synthesis pages.
- `AGENTS.md`, `index.md`, and `log.md` keep the process disciplined.

Treat raw documents as evidence. Treat the wiki as the current synthesized state.

## 1. Build a source inventory first

Before ingesting dozens or hundreds of files, create or update `raw/source-inventory.md`.

Suggested columns:

```markdown
| Source ID | File | Type | Topic | Project/System | Date | Owner/Team | Priority | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|
| SRC-0001 | raw/docs/example.md | Doc | Example topic | Example project | YYYY-MM-DD | Owner name | High | Not ingested | |
```

This inventory becomes the control panel for the wiki. It shows what exists, what matters, what has been ingested, and what still needs work.

## 2. Start with a small seed batch

Do not begin with hundreds of files. Pick 5 to 10 high-value sources first.

Good first sources include:

- Current project design docs.
- Architecture or system diagrams.
- Recent decision documents.
- Meeting notes where important tradeoffs were discussed.
- Onboarding docs that explain domain vocabulary.
- Documents people frequently ask about.

The first goal is to create the wiki spine:

- `wiki/Overview.md`
- `wiki/Current Priorities.md`
- `wiki/Open Questions.md`
- A few pages under `wiki/projects/`
- A few pages under `wiki/systems/`
- A few pages under `wiki/concepts/`
- A few pages under `wiki/decisions/`

## 3. Convert mixed formats into readable source text

Preserve the original file in `raw/`, then create an extracted markdown sidecar when needed.

Example:

```text
raw/docs/2026-06-22-example-design.docx
raw/docs/2026-06-22-example-design.extracted.md
```

Recommended handling by file type:

- Word documents: convert to markdown or plain text.
- PowerPoints: extract slide text, speaker notes, and image references.
- PDFs: extract text; use OCR if scanned.
- Screenshots: store the image under `raw/assets/`, then create a short markdown note describing what is visible.
- Architecture diagrams: store the original image or export, then create a companion explanation page.
- Mermaid, draw.io, or Visio diagrams: keep the original and export a viewable image or PDF when useful.

The LLM should ingest the extracted or readable version, while citing the original source path. Add small helper scripts under `tools/` (for example a Word or PDF extraction script) as the need arises.

## 4. Create one source summary per source

For every ingested source, create a page under `wiki/sources/` using [[templates/source-summary-template|the source summary template]].

Example:

```text
wiki/sources/SRC-0001 Example Design.md
```

Each source summary should include:

- One-line summary.
- Key takeaways.
- Systems, projects, decisions, concepts, teams, or diagrams affected.
- Important diagrams or screenshots.
- Open questions.
- Links back to raw files.
- Links forward to generated wiki pages.

The source summary is the bridge between immutable evidence and evolving synthesis.

## 5. Update durable wiki pages after each ingest

Do not stop at source summaries. The compounding value comes from updating reusable pages.

One document might update:

- `wiki/sources/SRC-0001 Example Design.md`
- `wiki/projects/Example Project.md`
- `wiki/systems/Example System.md`
- `wiki/concepts/Example Concept.md`
- `wiki/decisions/Use Example Approach.md`
- `wiki/diagrams/Example Sequence Diagram.md`
- `index.md`
- `log.md`

This is the key difference from basic document Q&A: the LLM is maintaining the current synthesized state rather than rediscovering knowledge every time.

## 6. Keep a human in the loop at first

For the first 10 to 20 ingests, ask the LLM to propose changes before editing many pages.

Useful prompt:

```text
Ingest this source into the wiki. First summarize what you think is important, then propose which wiki pages should be created or updated before editing.
```

Review the proposed page list. This tunes what counts as important for this wiki.

After several rounds, update `AGENTS.md` with naming conventions, taxonomy choices, confidentiality rules, and any preferences that emerge.

## 7. Treat diagrams and images as first-class sources

For architecture diagrams, screenshots, and exported whiteboards, use this pattern:

```text
raw/assets/example-sequence-v1.png
wiki/diagrams/Example Sequence Diagram.md
```

The diagram page should include:

- What the diagram shows.
- Which systems are involved.
- Main data or control flow.
- Assumptions.
- Unknowns.
- Related systems, projects, and decisions.
- Link to the image asset.

Images often contain important knowledge, but they are weakly searchable until they are explained in text.

## 8. Keep index.md useful

At moderate scale, `index.md` is the map that lets an LLM navigate the wiki without dedicated retrieval infrastructure.

Maintain it by category:

- Overview pages.
- Source summaries.
- Projects.
- Systems and architecture.
- Decisions.
- Concepts and terminology.
- People and teams.
- Meetings.
- Questions and analyses.
- Diagrams and assets.

Each durable wiki page should eventually have a one-line summary in the index.

Example:

```markdown
- [[wiki/systems/Example System]] - Short description of what it does and how it fits in.
```

## 9. Keep log.md as an audit trail

Every ingest, major query, lint pass, or maintenance pass should append a dated entry to `log.md`.

Example:

```markdown
## [2026-06-22] ingest | SRC-0001 Example Design

Ingested `raw/docs/2026-06-22-example-design.docx`.

Created:
- `wiki/sources/SRC-0001 Example Design.md`
- `wiki/systems/Example System.md`

Updated:
- `index.md`
- `wiki/projects/Example Project.md`

Open questions:
- Confirm whether the approach described here is still current.
```

This makes it possible to answer questions like "what changed recently?" or "why does the wiki say this?"

## 10. Run regular lint passes

After the first 20 or so sources, run a weekly or biweekly wiki health check.

Useful prompt:

```text
Run a wiki lint pass. Check for stale claims, missing cross-links, orphan pages, pages mentioned but not created, important systems without pages, diagrams without explanations, and contradictions between newer and older sources.
```

The lint pass should update:

- `wiki/Open Questions.md`
- `index.md`
- `log.md`
- Any stale pages that need correction.

## 11. Add search tooling only when needed

Start with simple navigation:

- Obsidian search.
- VS Code search.
- `index.md`.
- `log.md`.
- Plain markdown links.

At moderate scale (roughly 100 sources and hundreds of pages), this should work well if the index is maintained. Add local markdown search, BM25, vector search, or tools such as [qmd](https://github.com/tobi/qmd) only when the LLM starts missing obviously relevant pages.

## First week plan

1. Create `raw/source-inventory.md`.
2. Collect 10 high-value source files into `raw/docs/`, `raw/meetings/`, and `raw/assets/`.
3. Convert those files into extracted markdown sidecars where needed.
4. Ingest the first 2 documents interactively.
5. Review the generated wiki pages in Obsidian graph view.
6. Adjust `AGENTS.md` based on what worked and what did not.
7. Ingest 3 to 5 more sources.
8. Create or refine `wiki/Overview.md`, `wiki/Current Priorities.md`, and `wiki/Open Questions.md`.
9. Run the first lint pass and review `index.md` for usefulness.

## Default ingest prompt

Use this when adding a new source:

```text
Ingest this source into the wiki. Update the source summary, relevant project/system/concept/decision/diagram pages, index, and log. Flag contradictions and open questions. Preserve raw files as immutable sources.
```

This phrasing keeps the repo behaving like a living wiki instead of a folder of documents with chat layered on top.
