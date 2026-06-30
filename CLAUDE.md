# LLM Wiki — Schema & Operating Rules

This file is read by the agent at the start of every session. It is the source of
truth for structure, naming, and workflow. Update it whenever a convention changes —
never let it drift out of sync with reality.

## Model

Use the Anthropic API (remote), not a local model. The API key is expected in the
environment as `ANTHROPIC_API_KEY`. Long-context reasoning (reading multiple wiki
pages + a new source in one pass) is the point of using a remote model here — don't
artificially chunk things that fit in context.

## Directory roles

- `raw/inbox/` — append-only landing zone for new Markdown files (web clips, pasted
  articles, notes). I drop files here. You never edit a file in `raw/` — only read it.
- `raw/processed/` — after a file is ingested, move it here (`git mv`), unchanged.
  This is the permanent, immutable record of every source ever ingested.
- `wiki/concepts/` — one file per durable concept. This is the actual knowledge base.
- `wiki/sources/` — one file per ingested article: full citation, your summary, key
  quotes (paraphrased, not copied), and links to which concepts it touched.
- `wiki/questions/` — things you noticed are unclear, contradictory, or worth me
  following up on. Status field tracks open/resolved.
- `index.md` — single entry point. Lists all concepts and sources by category, kept
  current after every ingest. This is what gets read first, every session.
- `log.md` — newest entry at the top. One line per operation: what was ingested, what
  pages were created/updated, what questions were raised.

## Frontmatter conventions

Every page in `wiki/` starts with YAML frontmatter:

```yaml
---
title: "Human-readable title"
type: concept | source | question
status: draft | published
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag-one, tag-two]
related: ["concepts/other-concept.md"]
---
```

Source pages additionally include:

```yaml
source_url: "https://..."
source_date: YYYY-MM-DD   # original publish date if known
ingested: YYYY-MM-DD
```

## Filenames

Lowercase, kebab-case, no spaces, descriptive: `react-server-components.md`,
not `RSC.md` or `notes1.md`. Source pages are prefixed with the ingest date:
`2026-06-30-article-title-slug.md` — this keeps `raw/processed/` and
`wiki/sources/` naturally sorted chronologically.

## Internal linking

Use relative Markdown links only, never Obsidian wikilinks:

`[Server Components](../concepts/react-server-components.md)` — not `[[Server Components]]`.

This is required because the frontend (Next.js/Fumadocs) resolves standard Markdown
links, not Obsidian's wikilink syntax.

## Operations

### `ingest` — process one or more files in raw/inbox/

For each file in `raw/inbox/`:

1. Read it fully.
2. Identify: what concepts does this touch? Are any of them new, or do existing
   `wiki/concepts/*.md` pages already cover this territory?
3. For each new concept: create `wiki/concepts/<slug>.md` from the template.
4. For each existing concept that this source adds to, contradicts, or updates:
   edit that page. Don't just append — actually integrate the new information,
   resolve contradictions where you can, flag ones you can't in
   `wiki/questions/`.
5. Create one `wiki/sources/<date>-<slug>.md` page: summary, why it mattered,
   which concepts it updated.
6. Move the original file: `git mv raw/inbox/<file> raw/processed/<file>`.
7. Update `index.md`: add/update entries for every concept and source touched.
8. Prepend one entry to `log.md`:
   `YYYY-MM-DD HH:MM — ingested <file>; created/updated: <list>; questions raised: <n>`
9. Commit: `git add -A && git commit -m "ingest: <short description>"`.

If `raw/inbox/` has multiple files, process them one at a time, in order — don't
batch-read everything first, since later files may reference or update concepts
touched by earlier ones in the same session.

### `query` — answer a question using the wiki

1. Read `index.md` first to orient.
2. Read the specific concept pages relevant to the question — not the raw
   sources, unless the wiki pages explicitly point you back to one for a detail
   they don't capture.
3. Answer, citing which `wiki/` pages you drew from.
4. If the answer surfaces something genuinely new and durable, consider whether
   it's worth writing back into the wiki as a new page or page update — ask me
   before doing so for non-trivial additions.

### `lint` — periodic health check (run when I ask, or proactively suggest it
when raw/inbox/ has been empty for a while)

Check for: orphaned concept pages (nothing links to them and they link to
nothing), contradictions between pages that were never flagged as questions,
stale `status: draft` pages older than a few sessions, broken relative links,
and source pages with no corresponding concept updates (likely under-processed
ingests). Report findings, fix what's mechanical (broken links), flag what
needs human judgment as new `wiki/questions/` entries.

## What NOT to do

- Don't fetch URLs or browse the web during ingest — sources arrive pre-converted
  to Markdown in `raw/inbox/`. If a source references something you'd need to
  look up, note it as a question instead of guessing.
- Don't delete or edit files in `raw/processed/` — that's the immutable record.
- Don't create concept pages for one-off mentions — only for things that will
  plausibly be referenced again.
- Don't let `index.md` go stale — it must be updated in the same commit as any
  wiki change.
