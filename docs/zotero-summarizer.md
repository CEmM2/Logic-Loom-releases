# zotero-summarizer guide

Logic-Loom is built around the `zotero-summarizer` pipeline. If Logic-Loom is the loom, `zotero-summarizer` is the shuttle quietly doing the thread work.

## What zotero-summarizer does

`zotero-summarizer` turns a Zotero library plus local PDFs into an Obsidian-ready knowledge vault.

At a high level it can:

- read your Better BibTeX JSON export
- resolve PDFs from your Zotero data
- extract text from papers
- generate structured per-paper summaries
- synthesize collection-level digests
- publish the result as an interlinked markdown vault
- enrich the vault with citations, review-paper detection, and restructuring advice

## What Logic-Loom exposes

Inside Logic-Loom, the most important zsum flows are surfaced as desktop actions rather than CLI commands:

- extract / inspect text quality
- generate paper cards
- generate collection digests
- publish the vault
- watch logs while the pipeline runs
- inspect the generated markdown without leaving the app

## Newer zsum capabilities (in active testing)

The bundled `zotero-summarizer` recently gained several capabilities. They are
available through the CLI bundled with Logic-Loom today; Pipeline-UI surfacing
for some of them is still in progress.

- **NotebookLM pipeline** (`zsum nlm …`) — route card and digest generation
  through NotebookLM instead of a local LLM (`extraction.mode: notebooklm`), with
  automatic page-range fallback for papers NotebookLM fails on.
- **Section-aware extraction** (`extraction.mode: sections`) — extract the
  conceptually relevant TOC/heading-detected sections of each PDF rather than
  fixed page ranges, falling back to page ranges when too few sections are found.
- **Enrichment commands** — augment an existing vault without a full rerun:
  `zsum citations` (citation counts from OpenAlex + Semantic Scholar),
  `zsum reviews` (review/survey/tutorial detection), and `zsum restructure`
  (advisory on collection hierarchy).
- **Local-model setup** (`zsum setup-model --size small|medium|large|xlarge`) —
  one-command Ollama configuration that pulls a model and writes `config.yaml`.

The three extraction modes now available:

| Mode | Behaviour |
| --- | --- |
| `pages` (default) | First N + last M pages of each PDF |
| `sections` | TOC/heading-detected sections with fuzzy matching |
| `notebooklm` | Delegates to NotebookLM; page-range fallback on failure |

## What you still need before zsum can work

Even with the desktop app, the underlying research inputs still belong to you:

- **Zotero** installed and populated
- **Better BibTeX** export configured and kept up to date
- **Local PDFs** reachable from the exported metadata
- **An LLM backend or CLI** such as Ollama, LM Studio, Claude CLI, Codex CLI, Gemini CLI, NotebookLM, or another OpenAI-compatible endpoint

## Typical output

The published output is an Obsidian-style vault with content like:

- library index pages
- collection digest notes
- per-paper notes with structured summaries
- wikilinks between related notes

## Why this matters for release users

The desktop app bundles the zsum package, but it does **not** eliminate the need to configure your own library export, PDF locations, and model backend. Those are part of your local research environment and remain user-managed by design.

## Upstream docs

For full CLI, plugin, and architecture docs, see the upstream project:

- <https://github.com/SOSOVSKI/zotero-summarizer>
