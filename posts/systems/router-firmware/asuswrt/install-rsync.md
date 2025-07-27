---
title: RSYNCのインストール
description: ルーターでnginxを実行しています。\
authors:
  - XIYO
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:57:19+09:00
---
# RSYNCのインストール

ルーターでnginxを実行しています。\
ランディングページを構成中のため、自動デプロイのためにrsyncをインストールします。

## 環境

作業時の環境です。

- AC88U
- Merlin 386.12\_4
- Entware 2022-02-24

## 要件

必須要素です。詳細な説明は省略します。

- Merlinファームウェアのインストール
- Entwareのインストール
- jffsパーティションの有効化
- sshの有効化

## インストール

```bash
opkg update
opkg install rsync
```

