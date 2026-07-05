# GitHub Releases workflow

Logic-Loom uses a **two-repo release model**. A release is a single version tag
(`v*`) pushed to both repos; each repo's CI reacts to the tag differently.

| Repo | Workflow | On a `v*` tag push it… |
| --- | --- | --- |
| `SOSOVSKI/Logic-Loom` (private source) | `.github/workflows/release.yml` | cuts a **source-only** GitHub Release — `Logic-Loom-<ver>-source.{tar.gz,zip}` + `SHA256SUMS`. No binaries. |
| `CEmM2/Logic-Loom-releases` (this, public) | `.github/workflows/build-binaries.yml` | **builds the binaries** — checks out the private source at the tag via a PAT, builds macOS/Linux/Windows bundles on real runners, and attaches them (plus `SHA256SUMS.txt`) to the Release for that tag here. |

Both workflows read the release body from `dev/release_notes/<tag>.md` in the
source repo, and auto-mark `*-alpha` / `*-beta` / `*-rc` tags as prereleases.

## Latest release link

- <https://github.com/CEmM2/Logic-Loom-releases/releases/latest>

## What a public release contains

Each GitHub Release on this repo attaches:

- platform binaries/installers (macOS `.dmg`, Linux `.deb` + `.AppImage`, Windows `.msi` + NSIS `.exe`)
- a `SHA256SUMS.txt` manifest covering those assets
- the release notes as the body

Verify a download with:

```bash
shasum -a 256 -c SHA256SUMS.txt
```

## Required secret (this repo)

`build-binaries.yml` needs **`SOURCE_REPO_PAT`** — a fine-grained PAT with
**read** access to `SOSOVSKI/Logic-Loom` *Contents* — configured under
Settings → Secrets → Actions. It is used only to check out the private source at
the tag. The Release itself is created with the built-in `GITHUB_TOKEN`.

## Cutting a release

From the source repo, `scripts/release.sh` pushes the tag to both repos in order
(source first, then this mirror), idempotently:

```bash
bash scripts/release.sh --tag v0.1.0-alpha.7            # tag both repos → both workflows fire
bash scripts/release.sh --tag v0.1.0-alpha.7 --watch    # also watch the binary build here
bash scripts/release.sh --tag v0.1.0-alpha.7 --dry-run  # print the plan, change nothing
```

Add `dev/release_notes/<tag>.md` in the source repo before tagging — both
workflows use it as the release body.

## Repository layout

- `release-notes/<version>.md` — published release-note copy
- `checksums/<version>/` — checksum manifests from the older manual model (through alpha.5)
- `staging/<version>/` — staged binaries from the older manual model (through alpha.5)
- `docs/install.md` — stable install guidance
- `docs/known-issues.md` — cross-release caveats and limitations

> **Historical note:** through **alpha.5**, binaries were built in the source
> repo's CI, downloaded, and committed into this repo's `staging/` + `checksums/`
> folders by an older `scripts/release.sh`. As of the **alpha.6** cutover, CI in
> this repo builds the binaries and attaches them directly to the GitHub Release,
> so those folders are frozen historical artifacts rather than the live source of
> downloads. Always get binaries from the **Releases** page, not the repo tree.

## Why the split

The two-repo model cleanly separates **public binaries + user docs** from
**private implementation source**, and lets binaries build on public runners
without exposing the source tree — while still giving testers a stable, public
download target.
