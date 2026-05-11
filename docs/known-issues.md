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

## Platform parity is not guaranteed yet

Public releases may not ship every operating system on every tag.

Check the actual assets attached to the relevant GitHub Release rather than assuming that macOS, Windows, and Linux builds are always present together.

## Release-note rule of thumb

If a limitation is version-specific, it should also be repeated in that release's note under `release-notes/`.
