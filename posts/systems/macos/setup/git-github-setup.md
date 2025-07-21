---
title: Git Github Setup
authors:
  - XIYO
dates:
  - Thu Jul 17 2025 09:00:00 GMT+0900 (대한민국 표준시)
tags:
  - mac-setup
  - git
  - github
  - version-control
  - ssh
  - github-cli
---

# Git & GitHub 設定

> [!NOTE]
> **事前要件**
> [開発者必須ツールのインストール](step-01.md)が完了している必要があります。

## Git 基本設定

### ユーザー情報設定

Git コミットで使用される名前とメールアドレスを設定します。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

> [!TIP]
> GitHub アカウントと同じメールアドレスの使用を推奨します。
> 違っても構いませんが、誰がコミットしたかすぐに分かりにくくなります。

### デフォルトブランチ名設定

GitHub のデフォルトブランチ名と一致させます。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
git config --global init.defaultBranch main
```

> [!INFO]
> **なぜ Git はデフォルトブランチを master で作成し、GitHub は main で作成するのか？**
>
> 'master' という用語が master/slave（主人/奴隷）を連想させる可能性があるため、2020年から GitHub をはじめとする多くのサービスがより中立的な 'main' に変更しました。
>
> Git 自体は下位互換性を重視してまだデフォルトを変更していませんが、ユーザーが直接設定を変更できるオプションを提供しています。
> 上記のコマンドで Git のデフォルトブランチも 'main' に設定して GitHub と一致させることができます。

### 改行処理設定

Windows ユーザーとのコラボレーション時に改行文字の違いによる問題を防ぎます。
サーバーはほとんど Unix/Linux なので **Windows ユーザーが合わせるべきで、Mac/Linux ユーザー同士のみのコラボレーションではこの設定は不要**です。

他の OS とコラボレーションする場合のみ以下のコマンドを実行してください：

```bash
git config --global core.autocrlf input
```

> [!WARNING]
> **Windows ユーザー必須設定**
>
> コラボレーションプロジェクトに複数の OS が混在し Windows ユーザーがいる場合、
> **必ず Windows ユーザーのみ** `git config --global core.autocrlf true` を実行する必要があります。
> [!INFO]
> **改行の違いによる問題**
>
> Windows と Unix/Linux 間の改行方式が異なると、実際のコードは変更していないのに
> ファイル全体が修正されたようにステージに上がります。
>
> **なぜ問題になるのか？**
>
> - IntelliJ のような開発ツールは改行記号を表示しないため、何が変更されたか分かりません
> - チェックアウトのたびに改行が自動変換され、不要な変更が生じます
> - 実際のコード変更を見つけにくくなり、コードレビューが困難になります
>
> 上記の設定をすると、チェックアウト時に該当 OS に合わせて変換し、コミット時に Unix 方式（LF）に統一して
> このような混乱を防ぐことができます。

## GitHub CLI（gh）とは？

GitHub CLI は、ウェブブラウザを開かなくてもターミナルから直接 GitHub のすべての機能を使用できる公式ツールです。
PR 作成、イシュー管理、リポジトリクローンなどをコマンドで処理でき、開発フローを妨げません。

### GitHub CLI ログイン

GitHub CLI を使用するには、まず現在のコンピュータに GitHub 認証情報を保存する必要があります。
このプロセスを一度だけ行えば、以降すべての GitHub 作業を認証なしで実行できます。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
gh auth login
```

> [!INFO]
> **gh ログインの利点**
>
> GitHub CLI でログインすると、認証情報がシステムに安全に保存されます。
> その後 `git push` や `git pull` などのコマンド使用時：
>
> - 毎回ユーザー名とパスワードを入力する必要がありません
> - 複雑な Personal Access Token 発行プロセスを省略できます
> - ターミナルから直接 PR 作成、イシュー管理など GitHub 機能を使用できます
>
> でも CLI は不便だとブラウザばかり使う初心者たち 🥲

認証過程で選択するオプション：

1. **What account do you want to log into?** → GitHub.com
2. **What is your preferred protocol for Git operations?** → HTTPS
3. **Authenticate Git with your GitHub credentials?** → Y
4. **How would you like to authenticate GitHub CLI?** → Login with a web browser

### 認証確認

GitHub 認証が正常に完了したか確認します。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
gh auth status
```

## SSH キー設定

SSH（Secure Shell）は暗号化された通信のためのプロトコルです。
GitHub ではパスワードの代わりに SSH キーを使用してより安全で便利に認証できます。

> [!INFO]
> **SSH 設定はオプションです**
>
> - **gh CLI で HTTPS ですでに認証した場合**: 不要です
> - **SSH を好む場合**: 以下の手順に従って設定してください
> - **企業環境**: セキュリティを重視する環境では HTTPS を許可せず SSH のみ許可します

### SSH キーとは何か？

SSH キーはパスワードを代替するデジタル身分証です。
実際の鍵のように**秘密鍵**（private key）と**公開鍵**（public key）のペアで構成されます：

- **秘密鍵**: 自分のコンピュータにのみ保管する鍵（絶対に共有してはいけません！）
- **公開鍵**: GitHub に登録する錠前（共有しても安全）

GitHub に公開鍵を登録すると、自分のコンピュータの秘密鍵とペアが合う時のみアクセスを許可します。
まるで自分の鍵でのみ開く錠前を GitHub に設置するようなものです。

### SSH キー生成

新しい SSH キーを生成します。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Enter を 3 回押してデフォルト値で進めます。

> [!INFO]
> **コマンドオプション説明**
>
> - `-t ed25519`: 暗号化アルゴリズムタイプ指定（ed25519 は現在最も安全で速いアルゴリズム、最新 macOS のデフォルトなので省略可能）
> - `-C "your.email@example.com"`: キーを識別するためのコメント（省略時 Mac 名が自動的に入るので省略可能）
> [!WARNING]
> **SSH キーパスワードは設定しないでください！**
>
> SSH キー生成時にパスワードを設定できますが、初心者は絶対に設定しないことを推奨します。
> パスワードを忘れるとキーを使用できなくなり、とても苦労します。
>
> DevOps エキスパートになってからセキュリティ強化のためにパスワード設定を検討してください。
> （でもそんな状況は永遠に来ないかも...😅）

### キー生成後の確認

キー生成が完了すると `~/.ssh/` フォルダに 2 つのファイルが生成されます：

- `id_ed25519` - **秘密鍵**（絶対に共有禁止！）
- `id_ed25519.pub` - **公開鍵**（`.pub` 拡張子が付いているのが公開鍵）

> [!INFO]
> **macOS で SSH キーを確認する**
>
> これらのファイルは隠しフォルダにあるため Finder では見えません。
> ターミナルで `ls -la ~/.ssh/` で確認できます。

### SSH キーを GitHub に追加

生成した SSH 公開鍵を GitHub アカウントに追加します。

> [!INFO]
> **SSH キーを GitHub に追加するとは？**
>
> 先ほど生成した公開鍵（`id_ed25519.pub`）を GitHub アカウントに登録するプロセスです。
> これは GitHub サーバーに「この鍵（秘密鍵）を持っている人だけ私のアカウントへのアクセスを許可してください」と
> 錠前（公開鍵）を預けるようなものです。
>
> 登録後はターミナルで `git push`、`git pull` などを行う時
> パスワード入力なしで自動的に認証されます。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub --title "My Mac"
```

## 設定確認

すべての Git 設定が正しく行われたか確認します。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
git config --list
```

以下のような内容が表示されれば設定が正しく完了しています：

```text
user.name=Your Name
user.email=your.email@example.com
init.defaultbranch=main
core.autocrlf=input
```

> [!INFO]
> **設定確認ポイント**
>
> - `user.name` と `user.email` が正しく設定されている
> - `init.defaultbranch=main` でデフォルトブランチが設定されている
> - `core.autocrlf=input` で改行処理が設定されている（Windows ユーザーとのコラボレーション時）
>

## GitHub CLI でリポジトリ作成

設定が完了したら、gh コマンドで GitHub リポジトリを簡単に作成できます。

### 現在のディレクトリを GitHub にアップロード

> [!DANGER]
> **重要な情報がある場合は必ず private で作成してください！**
>
> API キー、パスワード、個人情報などが含まれるプロジェクトは必ず private リポジトリとして作成する必要があります。
> public で作成すると世界中の誰でも見ることができます。

```bash
# 現在のディレクトリを private リポジトリとして作成してすぐに push（デフォルト推奨）
gh repo create my-project --private --source=. --remote=origin --push
```

> [!INFO]
> **リポジトリ公開範囲オプション**
>
> - `--private`: 本人と招待された人のみ見ることができる（デフォルト推奨）
> - `--public`: 世界中の誰でも見ることができる
> - `--internal`: 組織内部メンバーのみ見ることができる（組織アカウント専用）

### 新しいリポジトリを作成してクローン

```bash
# GitHub にリポジトリを先に作成
gh repo create my-new-project --public --clone
```

### 便利な gh コマンド

```bash
# リポジトリリストを表示
gh repo list

# ブラウザでリポジトリを開く
gh repo view --web

# PR を作成
gh pr create

# イシューリストを表示
gh issue list
```

[戻る](step-01.md)