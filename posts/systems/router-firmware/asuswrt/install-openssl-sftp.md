---
title: ASUSWRTにOpenSSLとSFTPをインストールする
description: "`Dropbear`に`SFTP`機能を追加する方法を説明します。"
dates:
  - "2025-07-21T16:57:19.000Z"
  - "2025-07-21T16:33:12.000Z"
  - "2025-06-15T06:10:59.000Z"
  - "2024-09-08T03:40:36.000Z"
  - "2024-09-07T10:43:12.000Z"
authors:
  - XIYO
lastModified: 2025-07-26T11:55:48+09:00
---
# ASUSWRTにOpenSSLとSFTPをインストールする

`Dropbear`に`SFTP`機能を追加する方法を説明します。

`Dropbear`は`OpenSSH`の軽量パッケージです。\
`OpenSSH`の一部機能が削除され、`SFTP`も削除されました。

## 環境

- `ASUSWRT-MERLIN 386.12`
- `Entware armv7sf-k2.6`

## 方法

```bash
opkg update
opkg install openssh-sftp-server
```

パッケージマネージャの更新とインストールを行います。

インストール後は、他の設定を行わずにすぐにアクセスできます。

