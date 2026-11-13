# QQ for Linux 發行版鏡像

[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md)

本倉庫鏡像歸檔騰訊 QQ 官方 Linux 客戶端的歷史與最新安裝包，便於在官方下載地址失效或限速時取得。

`.deb`、`.rpm`、`.AppImage` 均取自騰訊官方下載源，未做任何修改。`.tar.xz` 由同版本 `amd64` 的 `.AppImage` 解包後重新打包生成。

## 下載

- 最新版本：前往 [Releases 最新頁](https://github.com/soloxiaoye2022/QQ-Linux/releases/latest)
- 歷史版本：前往 [全部 Releases](https://github.com/soloxiaoye2022/QQ-Linux/releases)

## 支援架構

| 架構 | 套件格式 | 說明 |
| --- | --- | --- |
| amd64 | `.deb` `.rpm` `.AppImage` `.tar.xz` | x86_64 桌面平台，含 tar 封存檔 |
| arm64 | `.deb` `.rpm` `.AppImage` | ARM64 桌面與開發板 |
| loongarch64 | `.deb` | 龍芯平台 |
| mips64el | `.deb` | 龍芯 MIPS 平台，官方自 3.2.34 起停止發佈 |

個別版本官方未發佈全部架構，例如 `3.2.30-50828` 僅有 `amd64` 與 `arm64` 的 `.deb`。以對應 Release 頁面實際列出的檔案為準。

## 檔案命名

```
QQ-<版本號>-<架構>.<副檔名>
```

範例：`QQ-3.2.35-54395-amd64.deb`

每個 Release 附帶 `SHA1SUMS` 校驗檔案。

## 校驗安裝包

```bash
# 下載 SHA1SUMS 後，在同一目錄執行
sha1sum -c SHA1SUMS
```

## 安裝

Debian / Ubuntu：

```bash
sudo apt install ./QQ-<版本號>-amd64.deb
```

Fedora / openSUSE：

```bash
sudo dnf install ./QQ-<版本號>-amd64.rpm
```

AppImage：

```bash
chmod +x QQ-<版本號>-amd64.AppImage
./QQ-<版本號>-amd64.AppImage
```

tar.xz 封存檔：

```bash
tar -xJf QQ-<版本號>-amd64.tar.xz
./qq/qq
```

## 版本來源

| 來源 | 涵蓋範圍 |
| --- | --- |
| 上游 [zydou/QQ-Linux](https://github.com/zydou/QQ-Linux) | 3.2.5 至 3.2.28，全部歷史資源原樣鏡像 |
| [flathub/com.qq.QQ](https://github.com/flathub/com.qq.QQ) 清單 | 3.2.33 起的版本號、官方下載地址與 sha256 校驗基準 |
| 騰訊官方 CDN | 3.2.33 及之後各架構安裝包 |
| [Rodert/qq-versions](https://github.com/Rodert/qq-versions) | 3.2.29、3.2.31、3.2.32 的完整架構歸檔 |

## 自動更新

倉庫內建三個 GitHub Actions 工作流：

| 工作流 | 作用 |
| --- | --- |
| `qq` | 每日檢查官方版本，有新版本時自動下載全部架構並發佈 |
| `backfill` | 依 `.github/qq-backfill.tsv` 清單補齊歷史缺失版本 |
| `mirror-upstream` | 將上游 zydou/QQ-Linux 的全部 Release 資源鏡像到本倉庫 |

新版本發佈前會校驗官方 sha256，校驗失敗即中止，避免發佈損壞檔案。

## 說明

本倉庫僅做鏡像分發，不提供任何修改、破解或二次打包的客戶端。QQ 客戶端版權歸騰訊所有。
