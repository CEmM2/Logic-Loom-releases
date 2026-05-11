# Logic-Loom overview

Logic-Loom is a desktop companion for the `zotero-summarizer` workflow. It wraps the underlying research pipeline in a local desktop interface so you can run stages, watch logs, inspect generated notes, and—when available—connect the output to AKMS-assisted knowledge workflows.

## What Logic-Loom does

| Area | What you can do |
| --- | --- |
| Pipeline | Run core zsum stages such as extraction, card generation, digests, and publish with live log output |
| Vault | Browse generated markdown, preview notes, resolve wikilinks, and search local content |
| Settings | Configure paths, caches, provider options, and other workflow settings |
| Graph | Explore a read-only AKMS graph view with filters, ego slices, cluster slices, and inspector actions |
| Picker / Nodes | Use optional AKMS workflows for paper batching, node generation, validation, and review |

## What is bundled in release builds

Release builds are intended to bundle the pieces a tester should not need to install manually:

- Logic-Loom desktop shell (Tauri + React)
- `logic-loom-api` Python sidecar
- `zotero-summarizer` package
- Python runtime dependencies required by the sidecar

## What is not bundled

Logic-Loom still depends on your research environment:

- Zotero
- Better BibTeX export
- local PDFs
- an LLM provider or local model service
- optional AKMS resources when using AKMS-specific tabs

That distinction matters: Logic-Loom reduces setup friction, but it does not install Zotero, locate your papers by magic, or log into model providers on your behalf.

## How Logic-Loom fits with zsum and AKMS

Logic-Loom sits between two layers:

1. **zotero-summarizer** — the pipeline that extracts paper text, generates per-paper cards, synthesizes collection digests, and publishes an Obsidian vault.
2. **AKMS** — an optional knowledge-graph layer for batch assignment, node generation, validation, and graph exploration.

If you only want the core summarization workflow, Logic-Loom can still be useful without AKMS.

## Current release posture

The public release track is still early-stage. Expect a few practical realities:

- install steps may still include alpha-quality warnings and manual confirmations
- first-run configuration can still surface expert-oriented settings
- AKMS-related tabs may be gated when the supporting packages or source vault are unavailable
- exact platform coverage depends on the current GitHub Release assets

For installation help, continue with the [install guide](install.md).
