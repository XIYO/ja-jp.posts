---
title: 開発者必須ツールのインストール
authors:
  - XIYO
tags:
  - mac-setup
  - developer-tools
  - git
  - docker
  - vscode
  - iterm2
  - jetbrains
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-23T00:41:04+09:00
---

# 開発者必須ツールのインストール

> [!NOTE]
> **事前要件**
> このガイドを進める前に [Homebrew のインストール](macos-step00-homebrew-installation)が完了している必要があります。

## 必須ツールのインストール

### 開発ツール

Git - 分散バージョン管理システム

```bash
brew install git
```

GitHub CLI - ターミナルから GitHub を使用

```bash
brew install gh
```

### ターミナル＆エディタ

iTerm2 - 強力なターミナルエミュレータ

```bash
brew install --cask iterm2
```

Visual Studio Code - Microsoft の無料コードエディタ

```bash
brew install --cask visual-studio-code
```

### 開発環境

Docker Desktop - コンテナベースの仮想化プラットフォーム

```bash
brew install --cask docker-desktop
```

JetBrains Toolbox - JetBrains IDE 管理ツール

```bash
brew install --cask jetbrains-toolbox
```

### フォント

D2Coding Nerd Font - 韓国語対応のコーディング専用フォント

```bash
brew install --cask font-d2coding-nerd-font
```

Pretendard - 読みやすさに優れた韓国語フォント

```bash
brew install --cask font-pretendard
```

> [!INFO]
> **Homebrew パッケージ名の変更事項**
>
> - **Docker**: `docker` → `docker-desktop`
> - **フォントリポジトリ**: 別途 tap 不要（メインリポジトリに統合）


## 追加設定

- **Git & GitHub CLI** → [Git & GitHub 設定ガイド](git-github-setup)
- **JetBrains Toolbox** → [JetBrains 設定ガイド](jetbrains-setup)
- **iTerm2 + Oh My Zsh** → [ターミナルカスタマイズガイド](terminal-customization)

## 次のステップ

必須ツールのインストールが完了しました。

[次のステップ：システムユーティリティのインストール](macos-step02-system-utilities)
