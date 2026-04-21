# Unlocks Wiki — Schema

A persistent, interlinked wiki of "AI Ed Unlocks" — research and engineering bets that, if pulled off, would unlock progress in K-12 education. Built per the pattern in [llm-wiki.md](./llm-wiki.md).

## Sources

The wiki's source of truth is a set of Padlet exports curated by Laurence Holt, plus contributor comments. Files live in `raw/`:

- `raw/Padlet - AI Ed Unlocks (1).pdf`
- `raw/Padlet - AI Ed Unlocks (2).pdf`
- `raw/Padlet - AI Ed Unlocks (3).pdf`

These are immutable. The wiki reads from them but never edits them.

## Layout

```
CLAUDE.md            # this file — schema and conventions
index.md             # catalog of all unlocks (read this first when answering)
log.md               # append-only chronological log of ingests / queries / lints
llm-wiki.md          # the upstream pattern this wiki implements
raw/                 # source PDFs (immutable)
assets/unlocks/     # one illustration per unlock, named <slug>.png
unlocks/            # one markdown page per unlock, named <slug>.md
```

## Slugs

Each unlock has a unique kebab-case slug taken from the Padlet card title (lowercased; `OTS-moves` becomes `ots-moves`). The slug is the filename stem for both the page (`unlocks/<slug>.md`) and its image (`assets/unlocks/<slug>.png`). Cross-references use Obsidian-style wikilinks: `[[adapted-lesson-eval]]`.

## Page format

Every unlock page follows the same structure so the catalog stays scannable. Frontmatter is YAML; body is markdown.

```markdown
---
slug: <slug>
title: <Human-Readable Title>
category: Eval | Dev | Research | Dataset | Agent | Measurement | Content | LLM resource
author: Laurence Holt
posted: YYYY-MM-DD
likes: <int>
comments: <int>
funder_interest: []     # populated later from funder transcripts
---

# <Human-Readable Title>

![<title>](../assets/unlocks/<slug>.png)

> <verbatim card description from Padlet>

**Use case.** <verbatim use-case statement from Padlet>

## Possible approach

- bullet
- bullet
- bullet

## Contributor notes

- <Author, date> — <verbatim comment / link>

## Related

- [[other-slug]]
```

The "Possible approach" section is the only place where the LLM expresses its own thinking about how the unlock might be solved. Keep it concise (3–6 bullets), action-oriented, and grounded in the unlock's category — Research bullets propose study designs, Dev bullets propose product/architecture moves, Dataset bullets propose collection methods, Eval bullets propose rubrics or benchmarks, etc.

## Categories

The Padlet uses these category tags. They're useful for grouping in the index and for shaping the "Possible approach" bullets:

- **Research** — empirical study or literature synthesis
- **Dev** — build a tool, prototype, or product
- **Eval** — define an evaluation/benchmark for a model or system
- **Dataset** — assemble a corpus to enable downstream research
- **Agent** — an autonomous LLM agent that acts over time
- **Measurement** — a new metric or instrument
- **Content** — curriculum or instructional material
- **LLM resource** — knowledge artifact (e.g., knowledge graph) usable by LLMs

## Workflows

**Ingest a new source.** Read the source. Discuss with the user. For each unlock the source touches: update its `unlocks/<slug>.md`, append to `## Contributor notes` with attribution and date, and (if relevant) add a `funder_interest:` entry. Update `index.md`. Append a row to `log.md`.

**Query.** Read `index.md` first to find candidate pages. Read those pages. Synthesize an answer with `[[wikilinks]]` and citations back to the source PDF + page. If the answer is a useful artifact (a comparison table, a thematic grouping, a shortlist), file it back into the wiki as a new page.

**Lint.** Look for: orphan pages, missing cross-references between obviously related unlocks, contradictions, stale claims, and unlocks the user is repeatedly asking about that should be promoted.

## Funder interest (forthcoming)

The user will paste in transcripts of conversations with funders. Per the workflow:

1. Read the transcript end-to-end.
2. Identify which unlocks each funder mentioned (by slug, name, or paraphrase).
3. For each match, append the funder's name + a short verbatim quote to the page's `## Funder interest` section (create it if absent), and add the funder name to the page's `funder_interest:` frontmatter.
4. Surface a ranked summary in `index.md` (e.g., "Top funder interest" section).

## Conventions

- Wikilinks use the slug, not the human title: `[[ai-personas]]` not `[[AI Personas]]`.
- Image paths are relative: `../assets/unlocks/<slug>.png`.
- Verbatim Padlet text and contributor comments are preserved as written; the LLM's commentary lives only in `## Possible approach`, `## Related`, and (later) `## Funder interest` summaries.
- Append-only log entries start with `## [YYYY-MM-DD] <verb> | <subject>` so they can be greppable.
