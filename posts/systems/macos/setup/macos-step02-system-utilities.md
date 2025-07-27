---
title: システムユーティリティのインストール
authors:
  - XIYO
tags:
  - mac-setup
  - productivity
  - slack
  - notion
  - obsidian
  - chrome
  - rectangle
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-23T00:41:04+09:00
---

# システムユーティリティのインストール

> [!NOTE]
> **事前要件**
> このガイドを進める前に [Homebrew のインストール](macos-step00-homebrew-installation)が完了している必要があります。

## 生産性ツールを一括インストール

開発とコラボレーションに必要な必須ツールをインストールします。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
(brew install --cask slack || true) && \
(brew install --cask notion || true) && \
(brew install --cask obsidian || true) && \
(brew install --cask google-chrome || true) && \
(brew install --cask rectangle || true) && \
echo "すべての生産性ツールのインストールが完了しました！"
```

> 正直に言って、私を信じてインストールしてください。
> 絶対に使うツールです。

## インストールしたツールの説明

### コラボレーション＆コミュニケーション

- **Slack** - チームコミュニケーションとコラボレーションのためのメッセンジャー。開発チーム必須ツール
- **Notion** - オールインワンワークスペース。ドキュメント、データベース、プロジェクト管理など

### ノート＆ドキュメント

- **Obsidian** - Markdown ベースの強力なノートアプリ。開発ドキュメントやメモ管理に最適

### ウェブブラウザ

- **Google Chrome** - 開発者ツールが強力なウェブブラウザ。ウェブ開発必須

### ウィンドウ管理

- **Rectangle** - ウィンドウのサイズと位置をキーボードで調整する無料ツール
  - `Ctrl + Option + ←/→`: 画面の半分を占有
  - `Ctrl + Option + ↑`: フルスクリーン
  - `Ctrl + Option + ↓`: ウィンドウを中央に配置

## 追加推奨ツール

開発スタイルに応じて選択的にインストールしてください。

## ツール別初期設定

### Rectangle 設定

1. Rectangle を起動
2. アクセシビリティ権限を許可
3. Preferences で「Launch on login」をチェック
4. 必要に応じてショートカットをカスタマイズ

### Chrome 設定

1. Chrome を起動してデフォルトブラウザに設定
2. 開発者ツールのショートカットを確認：`Cmd + Option + I`

### Slack 設定

1. ワークスペースを追加
2. 通知設定をカスタマイズ
3. ダークモードを設定（好みに応じて）

### Obsidian ウェブクリッパー設定

ウェブページを Obsidian に直接保存できる拡張機能です。

#### Chrome 用インストール

1. Chrome ウェブストアで「Obsidian Web Clipper」を検索
2. または直接インストール：[Obsidian Web Clipper - Chrome](https://chromewebstore.google.com/detail/obsidian-web-clipper/mphkdfmipddgfobjhphabphmpdckgfhb)
3. 拡張機能を追加後、Obsidian vault パスを設定

#### Safari 用インストール

1. Mac App Store で「Obsidian Clipper for Safari」を検索
2. または直接インストール：[Obsidian Clipper - Safari](https://apps.apple.com/app/obsidian-clipper-for-safari/id1640358805)
3. Safari → 設定 → 拡張機能で有効化
4. Obsidian vault パスを設定

> [!TIP]
> ショートカット設定：Chrome は `Cmd + Shift + O`、Safari は拡張機能設定で指定可能

## 次のステップ

システムユーティリティのインストールが完了しました。次はプログラミング言語別の開発環境を設定しましょう。

[次のステップ：プログラミング言語のインストール](macos-step03-programming-languages)
