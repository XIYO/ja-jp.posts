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
title: RSYNCのインストール
description: ルーターでnginxを実行しています。
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

