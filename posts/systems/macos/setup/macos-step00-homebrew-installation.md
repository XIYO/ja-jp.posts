---
title: Mac 初期設定ガイド
description: このガイドは Apple Silicon Mac 向けの開発環境設定ドキュメントです。Intel Mac の設定方法は扱いません。
authors:
  - XIYO
tags:
  - mac-setup
  - homebrew
  - apple-silicon
  - getting-started
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-23T00:41:04+09:00
---

# Mac 初期設定ガイド

このガイドは Apple Silicon Mac 向けの開発環境設定ドキュメントです。Intel Mac の設定方法は扱いません。

> [!INFO]
> **Mac プロセッサの確認方法**
> 
> 1. 画面左上の Apple ロゴをクリック
> 2. 「この Mac について」を選択
> 3. プロセッサ情報を確認：
>    - **Apple Silicon**: 「チップ」項目に Apple M1、M2、M3、M4 などと表示
>    - **Intel**: 「プロセッサ」項目に Intel Core i5、i7 などと表示

> [!WARNING]
> **Intel Mac ユーザーへの注意**
> 
> Intel プロセッサ Mac でこのガイドに従うと正常に動作しません。
> Apple Silicon (M1、M2、M3、M4) が確認できた場合のみ進めてください。

## Homebrew とは？

Homebrew は macOS 用のパッケージマネージャーです。App Store とは異なり、コミュニティが運営するオープンソースリポジトリで、開発者が必要とするツールやライブラリをコマンドラインから自由にインストール・管理できるようにします。

### Homebrew が必要な理由

開発ツールの多くは App Store で提供されていません。Git、Node.js、Python、Docker などの必須ツールは、それぞれのウェブサイトからダウンロードして複雑なインストール手順を踏む必要があります。Homebrew を使えば、これらすべてを簡単なコマンドで解決できます。

### 主な機能

- **パッケージインストール**: コマンド一つでプログラムをインストール
- **依存関係管理**: 必要なライブラリを自動的に一緒にインストール
- **バージョン管理**: インストール済みパッケージを最新版に保つ

## 始める前に

> [!NOTE]
> **ターミナルを開く**
> 1. `Cmd + Space` を押して Spotlight 検索を開きます
> 2. 「ターミナル」または「Terminal」と入力します
> 3. ターミナルアプリをクリックして実行します

## Homebrew のインストール

### インストール確認

Homebrew がすでにインストールされているか確認

```bash
if command -v brew &> /dev/null; then
    echo "Homebrew がすでにインストールされています。"
    brew --version
else
    echo "Homebrew がインストールされていません。"
fi
```

### Homebrew インストール

Homebrew インストールスクリプトを実行

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> [!NOTE]
> インストール過程で Mac ログインパスワードが要求されます。
> パスワード入力時に画面に表示されないのは正常です。

### 環境設定

Homebrew パスをターミナル設定ファイルに追加

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

現在のターミナルセッションに即座に適用

```bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```


### インストール確認

インストールが完了したか確認

```bash
brew --version
```

> [!TIP]
> バージョン情報が表示されれば、インストールが正常に完了しています。

> [!WARNING]
> **トラブルシューティング**
> - ターミナルを完全に終了して再起動
> - Mac を再起動
> - [Homebrew 公式ドキュメント](https://docs.brew.sh/Installation)を参照

## 次のステップ

Homebrew のインストールが完了しました。

[次のステップ：開発ツールのインストール](macos-step01-essential-developer-tools)
