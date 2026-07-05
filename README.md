# Meet The Logic-Loom

![banner image](./assets/banner.png)

> *It gathers the scrolls from the shelves in the hall, it thinks up the links that connect them all!*
>
> *It takes a messy math-scribble and turns it to speed, then watches the agents to ensure they succeed.*

Public home for downloadable Logic-Loom builds, release notes, install instructions, checksum manifests, and known issues.

Logic-Loom is a **three-mode desktop shell** for research workflows:

- **zsum** — a desktop front-end for the [zotero-summarizer](https://github.com/SOSOVSKI/zotero-summarizer) pipeline: run summarization stages, browse the published vault, inspect runs.
- **akms** *(gated)* — optional [AKMS](https://github.com/SOSOVSKI/AKMS) knowledge-graph tooling: batch node generation, a read-only graph explorer, a **Learn** tab, and a bundled **curated library of established nodes**.
- **assistant** — paper discovery across OpenAlex + Semantic Scholar, source batches, workflow runs, and a workspace-wide **⌘K / Ctrl-K** search.

Current release line: **v0.1.0-alpha.6**.

## Download

- Latest release: <https://github.com/CEmM2/Logic-Loom-releases/releases/latest>
- All releases: <https://github.com/CEmM2/Logic-Loom-releases/releases>

Release binaries live in **GitHub Releases**, not in this repo's tree and not in the private source repository. Each tagged release attaches macOS/Linux/Windows installers plus a `SHA256SUMS.txt` manifest.

## What lives in this repo

- `docs/` — public product docs, install guidance, AKMS/zsum context, and the release workflow
- `release-notes/` — published release notes by version
- `checksums/` — checksum manifests and verification guidance

> **Note:** the `staging/` and `checksums/` folders hold artifacts from the older manual release model (through alpha.5). As of the alpha.6 line, binaries are built by CI and attached directly to each GitHub Release — see [docs/github-releases.md](docs/github-releases.md).

## Start here

- [Logic-Loom overview](docs/logic-loom.md)
- [Install instructions](docs/install.md)
- [zotero-summarizer guide](docs/zotero-summarizer.md)
- [AKMS integration guide](docs/akms.md)
- [Known issues](docs/known-issues.md)
- [GitHub Releases workflow](docs/github-releases.md)

## What the app bundles

- Tauri desktop shell and React frontend
- Bundled `logic-loom-api` Python sidecar
- Bundled `zotero-summarizer` package and its Python runtime dependencies
- The vendored `akms` / `akms-nodes-gen` / `akms-learn` engines, so AKMS-gated tabs ship in the packaged app
- A curated, read-only library of **established** knowledge nodes (Tier A) plus ready-to-run **starter batches** (Tier B)

## What you still need

- Zotero
- Better BibTeX JSON export
- Access to your local PDFs
- An LLM backend or CLI — Ollama, LM Studio, an OpenAI-compatible endpoint, Claude CLI, Codex CLI, Gemini CLI, or NotebookLM
- An AKMS source vault only if you want the graph/Learn features

## Current release status

- Early alpha / pre-release quality
- Platform assets may vary by release — check the assets on the specific GitHub Release
- macOS Gatekeeper and Windows SmartScreen warnings are expected until signing/notarization is added
- Some onboarding flows still expose expert-oriented configuration fields inherited from the underlying research tooling
