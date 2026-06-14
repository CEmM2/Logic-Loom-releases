# GitHub Releases workflow

This repository is the public distribution point for Logic-Loom binaries.

## Latest release link

- <https://github.com/CEmM2/Logic-Loom-releases/releases/latest>

## What a release should contain

Each GitHub Release should bundle the user-facing materials that let someone download and trust the build:

- platform binaries/installers
- release notes
- checksum manifest
- install instructions
- known issues / caveats

That is why this repository keeps those materials in versioned markdown and checksum folders rather than burying them in the private implementation repo.

## Recommended release checklist

Before publishing a new release:

1. Build and smoke-test the platform artifact(s).
2. Copy or generate the final checksum manifest.
3. Update the matching file under `release-notes/`.
4. Confirm the release notes reflect the actual platform assets being uploaded.
5. Link to or summarize any important install notes and known issues.
6. Draft the GitHub Release and upload the assets plus checksum manifest.

Most of these steps are now automated by a single script in the implementation
repository (`scripts/release.sh`): it picks up the CI-built binaries, normalizes
their filenames, stages them plus checksum manifests into this release repo,
ships versioned copies of `README.md` and `CHANGELOG.md` as attached assets, and
creates the GitHub Release. The checklist above remains the underlying recipe.

## Suggested repository mapping

- `release-notes/<version>.md` — release body text to paste into GitHub Releases
- `checksums/<version>/SHA256SUMS.txt` — checksum manifest for that release
- `docs/install.md` — stable install guidance
- `docs/known-issues.md` — cross-release caveats and limitations

## Why keep releases here

The public release repo cleanly separates:

- **public binaries and user docs**
- **private or implementation-heavy source work**

That avoids sending testers to a source repository they may not be able to access and gives the project a stable, public download target.
