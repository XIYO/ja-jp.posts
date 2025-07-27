---
title: ASUSWRTにOpenSSLとSFTPをインストールする
description: "`Dropbear`に`SFTP`機能を追加する方法を説明します。"
authors:
  - XIYO
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:57:19+09:00
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

