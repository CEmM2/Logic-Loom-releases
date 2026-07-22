# Logic-Loom overview

Logic-Loom is a desktop companion for research workflows. It began as a front-end for the `zotero-summarizer` pipeline and has grown into a **three-mode desktop shell** that also covers optional AKMS knowledge-graph tooling and a research **Assistant** for paper discovery and workspace-wide search.

## The three modes

Logic-Loom presents a top-level mode switcher; every workflow belongs to one of three modes.

| Mode | What it covers |
| --- | --- |
| **zsum** | Run the `zotero-summarizer` pipeline (extract, cards, digests, publish), browse the published vault and collection hierarchy, and inspect past runs |
| **akms** *(gated)* | Optional AKMS knowledge-graph tooling: batch paper selection, node generation and validation, a read-only graph explorer, and the new **Learn** tab |
| **assistant** | Paper discovery across OpenAlex + Semantic Scholar, source batches, workflow runs, and a workspace-wide Cmd-K search |

AKMS mode is gated: its tabs appear only when the supporting AKMS packages and a readable source vault are available.

## What you can do

### zsum mode
- Run zsum stages (extract, cards, digests, publish, …) with live log streaming
- Browse and search the published Obsidian-style vault, with wikilink resolution
- Browse the collection hierarchy with digest- and card-state indicators
- Inspect and rerun previous pipeline runs
- *(in active testing)* route generation through **NotebookLM**, extract by **section** rather than fixed page ranges, run **enrichment commands** (citation counts, review-paper detection, structure advice), and configure a local Ollama model in one command

### akms mode *(gated)*
- **Picker** — group papers into batches and NotebookLM notebooks
- **Nodes** — browse, validate, and promote generated nodes
- **Graph** — explore the compiled AKMS graph (filters, ego/cluster slices, inspector)
- **Learn** *(in active testing)* — compile AKMS knowledge into learning artifacts; the UI is capability-driven, so generation modes and exporters come from the backend and any unavailable/planned mode renders disabled rather than failing on submit

### assistant mode
- **Discover** — search OpenAlex + Semantic Scholar and match results against your Zotero catalog
- **Related papers** — citations / references / similar / co-citation / co-reference exploration
- **Outputs** — browse, rerun, and compare workflow outputs
- **Workspace search** — Cmd-K / Ctrl-K across batches, discovered abstracts, zsum cards/digests, AKMS nodes, and workflow outputs

## What is bundled in release builds

Release builds bundle the pieces a tester should not need to install manually:

- Logic-Loom desktop shell (Tauri + React)
- `logic-loom-api` Python sidecar
- `zotero-summarizer` package and the Python runtime dependencies it needs
- the `akms-learn` engine, so the Learn modes ship in the packaged app
- a curated, read-only **library of established knowledge nodes** (Tier A) with provenance, plus ready-to-run **starter batches** (Tier B) seeded on first run
- the **MechDSL** executable bridge — compiles `% mechanics` LaTeX into FEM-solver code. It is bundled **Taichi-free**, so it adds this capability without the heavy Taichi runtime (an opt-in verify step can provision Taichi on demand, and is gated off by default)

## What is not bundled

Logic-Loom still depends on your research environment:

- Zotero
- Better BibTeX export
- local PDFs
- an LLM provider or local model service (Ollama, LM Studio, Claude / Codex / Gemini CLIs, NotebookLM, or another OpenAI-compatible endpoint)
- optional AKMS resources when using AKMS-gated tabs

That distinction matters: Logic-Loom reduces setup friction, but it does not install Zotero, locate your papers by magic, or log into model providers on your behalf.

## How Logic-Loom fits together

Logic-Loom sits across a few layers:

1. **zotero-summarizer** — extracts paper text, generates per-paper cards, synthesizes collection digests, and publishes an Obsidian vault.
2. **AKMS** — an optional knowledge-graph layer for batch assignment, node generation, validation, graph exploration, and (new) Learn artifacts.
3. **Assistant** — paper discovery and a workspace-wide search that tie the other layers together.

If you only want the core summarization workflow, Logic-Loom is still useful with just zsum.

## Current release posture

The current release line is **v0.1.0-alpha.7**. The feature arc through the recent alphas:

- **alpha.3** — Research Assistant (Learn), LLM providers, MechDSL bridge
- **alpha.4** — a **unified host-LLM provider** setting that drives Learn, zsum, and node generation from one place, plus packaged-app discovery of locally installed agent CLIs
- **alpha.5** — a bundled, gated **curated library of established nodes** (Tier A) and **starter batches** (Tier B), with a draft→established promotion path
- **alpha.6** — release-infrastructure cutover to the two-repo model (see [GitHub Releases workflow](github-releases.md)); no new app features
- **alpha.7** — the **Zotero pipeline runs in packaged builds again**: a frozen sidecar has no `python -m`, so every pipeline stage died at argument parsing on alpha.5/alpha.6. Bundled modules are now re-entered through a frozen-aware path, and a stale saved setting from those builds is repaired automatically. No UI or API surface changed.

It is still early-stage; expect a few practical realities:

- several capabilities (NotebookLM, section-aware extraction, enrichment commands, Learn) are shipped but **in active testing**
- install steps may still include alpha-quality warnings and manual confirmations
- first-run configuration can still surface expert-oriented settings
- AKMS and Learn tabs may be gated when the supporting packages, a readable source vault, or an LLM provider are unavailable
- exact platform coverage depends on the current GitHub Release assets

For installation help, continue with the [install guide](install.md).
