# QQ for Linux 发行版镜像

[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md)

本仓库镜像归档腾讯 QQ 官方 Linux 客户端的历史与最新安装包，便于在官方下载地址失效或限速时获取。

`.deb`、`.rpm`、`.AppImage` 均取自腾讯官方下载源，未做任何修改。`.tar.xz` 由同版本 `amd64` 的 `.AppImage` 解包后重新打包生成。

## 下载

- 最新版本：前往 [Releases 最新页](https://github.com/soloxiaoye2022/QQ-Linux/releases/latest)
- 历史版本：前往 [全部 Releases](https://github.com/soloxiaoye2022/QQ-Linux/releases)

## 支持架构

| 架构 | 包格式 | 说明 |
| --- | --- | --- |
| amd64 | `.deb` `.rpm` `.AppImage` `.tar.xz` | x86_64 桌面平台，含 tar 归档 |
| arm64 | `.deb` `.rpm` `.AppImage` | ARM64 桌面与开发板 |
| loongarch64 | `.deb` | 龙芯平台 |
| mips64el | `.deb` | 龙芯 MIPS 平台，官方自 3.2.34 起停止发布 |

个别版本官方未发布全部架构，例如 `3.2.30-50828` 仅有 `amd64` 与 `arm64` 的 `.deb`。以对应 Release 页面实际列出的文件为准。

## 文件命名

```
QQ-<版本号>-<架构>.<扩展名>
```

示例：`QQ-3.2.35-54395-amd64.deb`

每个 Release 附带 `SHA1SUMS` 校验文件。

## 校验安装包

```bash
# 下载 SHA1SUMS 后，在同一目录执行
sha1sum -c SHA1SUMS
```

## 安装

Debian / Ubuntu：

```bash
sudo apt install ./QQ-<版本号>-amd64.deb
```

Fedora / openSUSE：

```bash
sudo dnf install ./QQ-<版本号>-amd64.rpm
```

AppImage：

```bash
chmod +x QQ-<版本号>-amd64.AppImage
./QQ-<版本号>-amd64.AppImage
```

tar.xz 归档：

```bash
tar -xJf QQ-<版本号>-amd64.tar.xz
./qq/qq
```

## 版本来源

| 来源 | 覆盖范围 |
| --- | --- |
| 上游 [zydou/QQ-Linux](https://github.com/zydou/QQ-Linux) | 3.2.5 至 3.2.28，全部历史资源原样镜像 |
| 腾讯官方下载文档页 | 3.2.33 及之后各架构安装包的官方直链 |
| [Rodert/qq-versions](https://github.com/Rodert/qq-versions) | 3.2.29、3.2.31、3.2.32 的完整架构归档 |

## 自动更新

仓库内置三个 GitHub Actions 工作流：

| 工作流 | 作用 |
| --- | --- |
| `qq` | 每日检查腾讯官方文档页，有新版本时自动下载全部架构并发布 |
| `backfill` | 按 `.github/qq-backfill.tsv` 清单补齐历史缺失版本 |
| `mirror-upstream` | 将上游 zydou/QQ-Linux 的全部 Release 资源镜像到本仓库 |

`qq` 工作流只以腾讯官方域名（`docs.qq.com`、`qqdl.gtimg.cn`）作为版本与安装包来源，不依赖任何第三方仓库。下载后会校验安装包结构（deb 的 ar 魔数、rpm 的 rpm 魔数、AppImage 的 ELF 头），校验失败即中止，避免发布损坏文件。

## 说明

本仓库仅做镜像分发，不提供任何修改、破解或二次打包的客户端。QQ 客户端版权归腾讯所有。
