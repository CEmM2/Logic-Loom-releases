# Known issues

This page tracks current cross-release caveats for Logic-Loom public builds.

## Installation and trust warnings

- **macOS Gatekeeper:** early alpha builds may be unsigned or not yet notarized, so first launch can require the right-click → **Open** path.
- **Windows SmartScreen:** unsigned builds can trigger trust warnings until code signing is added.

## First-run setup still feels technical

Some alpha builds may still expose configuration fields or path prompts that reflect the underlying research tooling more than a polished consumer installer.

Typical examples:

- manual file/path selection
- terminology inherited from `zotero-summarizer`
- optional AKMS-specific path fields that only matter for advanced users

## External dependencies are still external

Logic-Loom does **not** bundle:

- Zotero
- Better BibTeX configuration
- your PDFs
- authentication for external LLM CLIs or services

If those pieces are missing or misconfigured, the desktop app can only be as happy as its inputs.

## AKMS availability varies

AKMS-related tabs and workflows are optional. Depending on the release and your local setup:

- AKMS tabs may be gated
- graph features may need a readable source vault
- batch/node workflows may require separate AKMS resources

## Several newer features are in active testing

As of **v0.1.0-alpha.3**, a number of capabilities are shipped but still being
exercised. Treat them as evolving:

- **Research Assistant — Learn** — the Learn tab and its generation modes are
  new; available modes and exporters are driven by the backend, and some need a
  host-supplied LLM provider (without one, those modes are disabled).
- **NotebookLM pipeline / section-aware extraction / enrichment commands** — the
  newer `zotero-summarizer` flows are available via the bundled CLI; Pipeline-UI
  surfacing for some of them is still in progress.
- **NotebookLM** in particular requires you to be signed in to Google in the
  environment NotebookLM uses; Logic-Loom does not manage that authentication.
- **MechDSL** emit/transpile works out of the box, but the optional
  verification step needs a Taichi runtime that is **not bundled** and is gated
  off by default.

## Platform parity is not guaranteed yet

Public releases may not ship every operating system on every tag.

Check the actual assets attached to the relevant GitHub Release rather than assuming that macOS, Windows, and Linux builds are always present together.

## Release-note rule of thumb

If a limitation is version-specific, it should also be repeated in that release's note under `release-notes/`.
