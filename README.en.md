# QQ for Linux Releases Mirror

[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md)

This repository mirrors and archives historical and current installers for the official Tencent QQ Linux client, so they remain obtainable when official download URLs expire or throttle.

All `.deb`, `.rpm` and `.AppImage` files come from Tencent's official download sources, unmodified. Each `.tar.xz` is produced by extracting the matching `amd64` `.AppImage` and repacking it.

## Download

- Latest version: see the [latest release](https://github.com/soloxiaoye2022/QQ-Linux/releases/latest)
- Historical versions: see [all releases](https://github.com/soloxiaoye2022/QQ-Linux/releases)

## Supported architectures

| Architecture | Package formats | Notes |
| --- | --- | --- |
| amd64 | `.deb` `.rpm` `.AppImage` `.tar.xz` | x86_64 desktop, includes the tar archive |
| arm64 | `.deb` `.rpm` `.AppImage` | ARM64 desktops and development boards |
| loongarch64 | `.deb` | Loongson platform |
| mips64el | `.deb` | Loongson MIPS platform, no longer published by Tencent since 3.2.34 |

## File naming

```
QQ-<version>-<arch>.<extension>
```

Example: `QQ-3.2.35-54395-amd64.deb`

Every release ships a `SHA1SUMS` checksum file.

## Verify a package

```bash
# Download SHA1SUMS into the same directory, then run
sha1sum -c SHA1SUMS
```

## Install

Debian / Ubuntu:

```bash
sudo apt install ./QQ-<version>-amd64.deb
```

Fedora / openSUSE:

```bash
sudo dnf install ./QQ-<version>-amd64.rpm
```

AppImage:

```bash
chmod +x QQ-<version>-amd64.AppImage
./QQ-<version>-amd64.AppImage
```

tar.xz archive:

```bash
tar -xJf QQ-<version>-amd64.tar.xz
./qq/qq
```

## Version provenance

| Source | Coverage |
| --- | --- |
| Upstream [zydou/QQ-Linux](https://github.com/zydou/QQ-Linux) | 3.2.5 through 3.2.28, all historical assets mirrored as-is |
| [flathub/com.qq.QQ](https://github.com/flathub/com.qq.QQ) manifest | Version numbers, official download URLs and sha256 baselines from 3.2.33 onward |
| Tencent official CDN | Per-architecture packages for 3.2.33 and later |
| [Rodert/qq-versions](https://github.com/Rodert/qq-versions) | Full architecture archives for 3.2.29, 3.2.31 and 3.2.32 |

## Automated updates

Three GitHub Actions workflows keep this repository current:

| Workflow | Purpose |
| --- | --- |
| `qq` | Checks for a new official version daily, downloads every architecture and publishes it |
| `backfill` | Fills historical gaps listed in `.github/qq-backfill.tsv` |
| `mirror-upstream` | Mirrors every release asset from upstream zydou/QQ-Linux into this repository |

New releases are gated on Tencent's official sha256; a mismatch aborts the run instead of publishing a corrupt file.

## Notes

This repository only mirrors and distributes packages. It provides no modified, cracked or repackaged clients. The QQ client is copyright Tencent.
