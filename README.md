# LLM Wiki

A personal, LLM-maintained knowledge base. This is **not** a RAG app. It is a
*compiled* knowledge base: instead of re-deriving answers from raw sources on every
query, an agent (Claude Code) reads each new source once, extracts and synthesizes what
matters, and writes durable Markdown pages. The wiki accumulates and improves over time
instead of starting from scratch each session.

Core philosophy: **the file tree is the IDE, the agent is the programmer, the wiki is
the codebase.**

## Repository structure

```
.
├── CLAUDE.md         schema + operating rules the agent reads every session
├── README.md         this file
├── index.md          content catalog — entry point for humans and the agent
├── log.md            prepend-only chronological log of every operation
├── raw/
│   ├── inbox/        drop new .md files here (Obsidian Web Clipper or manual paste)
│   └── processed/    immutable record of ingested sources (never edited)
├── wiki/
│   ├── concepts/     one page per durable concept — the actual knowledge base
│   ├── sources/      one page per ingested article (citation + summary)
│   └── questions/    open questions flagged during ingest
├── templates/        page templates for concepts, sources, questions
└── scripts/          notes on any helper scripts
```

## Adding a source

1. Clip an article with Obsidian Web Clipper (or paste one manually) as a `.md` file
   into `raw/inbox/`.
2. Tell the agent `ingest` (or it will notice new files and ask).
3. The agent reads the source, creates/updates concept pages, writes a source page,
   moves the original to `raw/processed/`, updates `index.md`, logs the operation, and
   commits.
4. Review the diff and push to GitHub.

## Operations

See [CLAUDE.md](CLAUDE.md) for the full schema. The main operations are:

- **`ingest`** — process the files in `raw/inbox/` into wiki pages.
- **`query`** — answer a question using the compiled wiki pages.
- **`lint`** — health check for orphans, contradictions, stale drafts, broken links.

## Frontend

A separate Next.js application (Fumadocs-based) reads `wiki/` and `index.md` from this
repo directly for navigation and rendering. Because of this:

- All content is plain Markdown with YAML frontmatter.
- Internal links are **relative Markdown links**
  (`[Concept](../concepts/concept.md)`), never Obsidian `[[wikilinks]]`.
- Filenames are lowercase-kebab-case with no spaces.
