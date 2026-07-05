# Logic-Loom documentation

This repository is the public documentation and binary-distribution home for Logic-Loom.

Logic-Loom is a **three-mode desktop shell** — `zsum` (the research pipeline),
`akms` (optional knowledge-graph tooling, including the **Learn** tab and a
bundled curated node library), and `assistant` (paper discovery + workspace
search). The current release line is **v0.1.0-alpha.6**; grab whatever is newest
from [Releases](https://github.com/CEmM2/Logic-Loom-releases/releases/latest).

Use the pages below depending on what you need:

| Page | What it covers |
| --- | --- |
| [Logic-Loom overview](logic-loom.md) | What the desktop app does, what it bundles, and where it fits in the workflow |
| [Install instructions](install.md) | Downloading, installing, and first-launch setup for release builds |
| [zotero-summarizer guide](zotero-summarizer.md) | The research pipeline Logic-Loom wraps and streamlines |
| [AKMS integration guide](akms.md) | Optional AKMS concepts, batch tooling, graph features, and current limits |
| [Known issues](known-issues.md) | Current release caveats and rough edges |
| [GitHub Releases workflow](github-releases.md) | Where binaries live and how release artifacts are organized |

## What this repo is for

The public release repo is intentionally lightweight:

- **GitHub Releases** host the binaries
- **`release-notes/`** stores the versioned release-note markdown
- **`checksums/`** stores checksum manifests and verification guidance
- **`docs/`** gives public-facing product and install documentation

For the underlying upstream projects, see:

- [zotero-summarizer](https://github.com/SOSOVSKI/zotero-summarizer)
- [AKMS](https://github.com/SOSOVSKI/AKMS)
