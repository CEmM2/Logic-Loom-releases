# Install instructions

These steps are for **release builds** downloaded from GitHub Releases, not for developers cloning the source repository.

## Before you install

Logic-Loom is a desktop companion, not a full research environment in a box. You still need:

- Zotero
- Better BibTeX export configured in Zotero
- access to your local PDFs
- an LLM backend or provider CLI

Depending on the current alpha, you may also need to supply a few expert-style paths during first-run setup.

## Download

Get the latest release from:

- <https://github.com/CEmM2/Logic-Loom-releases/releases/latest>

Each GitHub Release should include:

- one or more platform installers/binaries
- release notes
- checksum manifest
- install notes / known issues

Not every alpha will ship every platform on day one. If your target platform
is not published yet and you have source access, the advanced Linux / Windows
build notes below explain how to package Logic-Loom locally on that OS.

## macOS

1. Download the `.dmg` for your architecture.
2. Open the disk image.
3. Drag `Logic-Loom.app` into `Applications`.
4. Launch the app from `Applications`.

### If macOS warns about an unidentified developer

Because early alpha builds may not yet be signed/notarized, macOS can block the first launch.

Try this first:

1. Right-click `Logic-Loom.app`
2. Click **Open**
3. Confirm **Open**

If Gatekeeper still blocks launch, advanced users can remove quarantine flags manually:

```bash
xattr -dr com.apple.quarantine /Applications/Logic-Loom.app
```

## Windows

1. Download the installer or packaged `.exe` from the release page.
2. Run it.
3. If SmartScreen appears, choose the advanced option and continue only if you trust the release source.

Unsigned alpha builds can trigger SmartScreen warnings until code signing is added.

### Build from source on Windows

If a Windows asset is not available for your target alpha and you have source
access, build **on Windows** rather than cross-compiling from another OS.

Prerequisites:

- Node.js 20+
- pnpm 11
- Rust stable with the MSVC toolchain
- Visual Studio C++ Build Tools
- Microsoft Edge WebView2 runtime
- `uv`
- a sibling checkout of `zotero-summarizer` at `..\zotero-summarizer`

From PowerShell in the source repo root:

```powershell
pnpm install
pnpm logic-loom:package:windows
```

That flow freezes the bundled Python sidecar with `uv`, then builds the Tauri
desktop package. Resulting installers land under:

- `apps/desktop/src-tauri/target/release/bundle/nsis/`
- `apps/desktop/src-tauri/target/release/bundle/msi/`

## Linux

Platform assets may vary by release. If an AppImage is provided:

1. Download the `.AppImage`.
2. Mark it executable.
3. Launch it.

```bash
chmod +x Logic-Loom-*.AppImage
./Logic-Loom-*.AppImage
```

If a `.deb` or other package is provided in a later release, prefer the instructions packaged with that specific release.

### Build from source on Linux

If no Linux artifact is published yet and you have source access, build on a
Linux machine with the native packaging dependencies installed.

Typical prerequisites:

- Node.js 20+
- pnpm 11
- Rust stable
- `uv`
- a sibling checkout of `../zotero-summarizer`
- distro packages for the Tauri GTK/WebKit stack such as `build-essential`,
  `pkg-config`, `libgtk-3-dev`, `libwebkit2gtk-4.1-dev`,
  `libayatana-appindicator3-dev`, `librsvg2-dev`, and `patchelf`

From the source repo root:

```bash
pnpm install
pnpm logic-loom:package:linux
```

That builds the sidecar with `uv` and packages the desktop app for the current
Linux host. The resulting artifacts usually land under:

- `apps/desktop/src-tauri/target/release/bundle/appimage/`
- `apps/desktop/src-tauri/target/release/bundle/deb/`

## First launch checklist

After the app opens, be ready to confirm or configure:

- your Better BibTeX JSON export path
- your Zotero database / PDF paths as needed by the current alpha
- your target output vault or working directories
- your preferred LLM backend or CLI
- optional AKMS paths only if you want AKMS-specific features

## If something still feels too developer-ish

That is a known alpha limitation rather than you doing something wrong.

See:

- [Known issues](known-issues.md)
- [zotero-summarizer guide](zotero-summarizer.md)
- [AKMS integration guide](akms.md)
