# Log

Append-only chronological record of wiki operations. Entries start with `## [YYYY-MM-DD] <verb> | <subject>` so the log is greppable: `grep "^## \[" log.md | tail -10`.

## [2026-04-21] bootstrap | wiki initialized from Padlet PDFs

Created the schema (`CLAUDE.md`), index (`index.md`), and one page per unlock under `unlocks/`. Source: `raw/Padlet - AI Ed Unlocks (1|2|3).pdf`. Extracted 53 illustrations into `assets/unlocks/<slug>.png`. Each unlock page captures the verbatim Padlet description + use case, contributor comments, and a "Possible approach" section with the LLM's own thinking on how the unlock might be solved. The `funder_interest:` frontmatter and `## Funder interest` sections are stubs — to be populated when funder transcripts are ingested.
