# Checksums

Store release checksum manifests under a versioned subfolder.

Recommended layout:

```text
checksums/
  v0.1.0-alpha.1/
    SHA256SUMS.txt
```

## Generate checksums

### macOS / Linux

```bash
shasum -a 256 * > SHA256SUMS.txt
```

If `shasum` is unavailable on Linux:

```bash
sha256sum * > SHA256SUMS.txt
```

### Windows PowerShell

```powershell
Get-FileHash .\Logic-Loom-*.exe -Algorithm SHA256
```

For multiple Windows assets, export each hash into a plain text manifest matching the filenames attached to the release.

## Verify checksums

### Verify on macOS / Linux

```bash
shasum -a 256 -c SHA256SUMS.txt
```

### Verify on Windows PowerShell

Compare `Get-FileHash` output against the published manifest.

## Important

Checksums must match the **final uploaded asset filenames**. If you rename an installer after generating the manifest, regenerate the manifest too.
