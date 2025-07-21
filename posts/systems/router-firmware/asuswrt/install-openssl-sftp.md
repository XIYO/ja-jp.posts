---
authors:
  - XIYO
  - XIYO
dates:
  - '2024-09-08T12:40+0900'
  - '2024-09-07T19:43+0900'
messages:
  - ':art: 로케일 코드 제거하고, 번역된 파일을 기존 처럼 /static/{locale} 구조로 저장'
  - ':globe_with_meridians: 일본어 추가'
title: ASUSWRTにOpenSSLとSFTPをインストールする
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

