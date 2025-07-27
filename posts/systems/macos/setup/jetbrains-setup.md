---
title: JetBrains 設定ガイド
authors:
  - XIYO
tags:
  - mac-setup
  - jetbrains
  - intellij
  - ide
  - development-tools
  - font-settings
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T02:44:45+09:00
---

# JetBrains 設定ガイド

## JetBrains とは？

JetBrains はチェコのソフトウェア開発会社で、開発者の生産性を最大化する IDE（統合開発環境）を作ることで有名です。
IntelliJ IDEA（Java）、PyCharm（Python）、WebStorm（JavaScript）、GoLand（Go）など言語別に特化した IDE を提供しています。

世界中の開発者が最も好む IDE の一つで、スマートなコード補完、強力なデバッグ、リファクタリングツールを提供します。

## JetBrains Toolbox とは？

JetBrains Toolbox は JetBrains のすべての IDE を一箇所で管理できるデスクトップアプリです。
まるで App Store のように IDE をインストール、アップデート、削除でき、複数のバージョンを同時に管理できます。

### Toolbox でインストールすべき理由

**独立してインストールする時の問題点：**

- 各 IDE を個別にダウンロードしてインストールする必要がある
- アップデートを手動で確認してインストールする必要がある
- ライセンスをそれぞれ管理する必要がある
- 複数バージョンの管理が複雑

**Toolbox 使用の利点：**

- すべての IDE を一箇所で統合管理
- 自動アップデート対応
- 一つのライセンスですべての IDE 使用
- プロジェクトごとに異なる IDE バージョン使用可能
- ターミナルから IDE 実行のための shell script 自動生成

## JetBrains Toolbox 初期設定

### Toolbox 実行

JetBrains Toolbox アプリを実行するコマンドです。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
open -a "JetBrains Toolbox"
```

> [!INFO]
> **macOS セキュリティ承認必要**
>
> 初回実行時に「JetBrains Toolbox を開いてもよろしいですか？」のようなセキュリティダイアログが表示されます。
> 「開く」をクリックして承認してください。

### ログイン

JetBrains アカウントでログインします。アカウントがない場合は [JetBrains アカウント作成](https://account.jetbrains.com/login)で先にアカウントを作成してください。

## IntelliJ IDEA Ultimate のインストール

IntelliJ IDEA は JetBrains の代表的な Java IDE です。Community（無料）と Ultimate（有料）の 2 つのバージョンがあります：

- **Community Edition**: 基本的な Java 開発機能提供（無料）
- **Ultimate Edition**: ウェブ開発、データベース、フレームワーク対応など高度な機能含む（有料、学生無料）

**IntelliJ IDEA Ultimate に含まれる主要機能：**

- **ウェブ開発**: JavaScript、TypeScript、React、Vue.js、Angular 対応
- **データベース**: DataGrip のすべての機能内蔵（MySQL、PostgreSQL、MongoDB など）
- **フレームワーク**: Spring、Spring Boot、Hibernate、JPA 対応
- **バージョン管理**: Git、SVN、Mercurial 高度な機能
- **クラウド**: Docker、Kubernetes、AWS、Google Cloud 対応
- **テスト**: JUnit、TestNG、Mockito 統合対応

Ultimate 一つで Java バックエンドから React フロントエンド、データベース作業まですべての開発ができます。

> コミュニティバージョンは無料とは言うけど、必要な機能一つ一つが Ultimate にしかなくて使わない方が精神衛生上良いという噂が... 🤒

### インストール

Toolbox で **IntelliJ IDEA Ultimate** を探して Install をクリックします。

### ライセンス有効化

IntelliJ IDEA Ultimate を使用するにはライセンスが必要です。3 つのオプションがあります：

#### 30日無料体験

- 別途申請なしですぐに 30 日間使用可能
- 体験期間中すべての機能使用可能

#### 学生無料ライセンス

- 学生認証時に卒業まで無料使用
- [JetBrains 学生ライセンス申請](https://www.jetbrains.com/student/)
- 学校メールまたは学生証で認証

#### 有料サブスクリプション

- **個人**: 月 $17 / 年 $169（1年目） → $135（2年目） → $101（3年目以降）
- **企業**: 月 $60 / 年 $599（ユーザーあたり）

> [!INFO]
> **連続サブスクリプション割引特典**
>
> JetBrains は連続サブスクリプションに対して割引を適用します。学生認証で使用した期間も
> 後で有料サブスクリプション転換時に使用期間に含まれて割引特典を受けることができます。
>
> **体験版で開始**: 30日体験 → 学生ライセンス（無料） → 有料サブスクリプション（割引適用）の順序を推奨します。

## IntelliJ 必須ショートカット

IntelliJ の生産性を最大化する必須ショートカットです。これらだけ習得しても開発速度が大幅に向上します。

### 検索関連（最も重要！）

- `Double Shift` - すべてを検索（ファイル、クラス、メソッド、設定など）
- `Cmd + Shift + A` - すべてのアクションを検索（メニュー、機能を探す）
- `Cmd + Shift + F` - プロジェクト全体でテキスト検索
- `Cmd + F` - 現在のファイルで検索
- `Cmd + R` - 現在のファイルで置換

### ファイルおよびナビゲーション

- `Cmd + E` - 最近開いたファイルリスト
- `Cmd + Shift + E` - 最近編集したファイルリスト
- `Cmd + O` - クラスに移動
- `Cmd + Shift + O` - ファイルに移動
- `Cmd + Alt + O` - シンボル（メソッド、変数）に移動

### コード編集

- `Cmd + D` - 現在の行を複製
- `Cmd + X` - 現在の行を切り取り（選択範囲なしで）
- `Cmd + /` - 1行コメントトグル
- `Cmd + Shift + /` - ブロックコメントトグル
- `Alt + Up/Down` - メソッド単位で移動
- `Cmd + Shift + Up/Down` - コードブロック移動

### 実行およびデバッグ

- `Ctrl + R` - 実行
- `Ctrl + D` - デバッグ実行
- `F8` - デバッグ時に次の行に移動
- `F7` - デバッグ時にメソッド内に入る
- `Shift + F8` - デバッグ時にメソッドから出る

### リファクタリング

- `Shift + F6` - 名前変更（変数、メソッド、クラス）
- `Cmd + Alt + M` - メソッド抽出
- `Cmd + Alt + V` - 変数抽出
- `Cmd + Alt + L` - コードフォーマット

> [!TIP]
> **ショートカット学習のヒント**
>
> 最初は `Double Shift` と `Cmd + Shift + A` だけ覚えても大丈夫です。
> この 2 つだけですべての機能にアクセスでき、使いながら自然に他のショートカットも習得できます。

## D2Coding Nerd Font 設定

> [!INFO]
> **D2Coding Nerd Font 事前インストール確認**
>
> D2Coding Nerd Font は韓国語対応と開発者アイコンをすべてサポートするフォントです。
> macos-step01-essential-developer-tools.md ですでにインストールしたので設定のみ進めればよいです。

### エディタフォント設定

IntelliJ IDEA → Settings（`Cmd+,`） → Editor → Font で次のように設定します：

- Font: **D2CodingLigature Nerd Font**
- Size: **14**（推奨）
- Line height: **1.2**
- Enable ligatures: ON（コード可読性向上）

> [!INFO]
> **Nerd Font**: 開発者のために特別に製作されたフォントで、一般フォントに Git 状態、ファイルタイプ、ディレクトリなどを表す
> 数千個のアイコンが追加されたフォントです。ターミナルテーマや IDE でファイルアイコン、ブランチ表示などがきれいに表示されます。
>
> **Ligatures**: 連続した文字を一つの記号に結合して表示する機能です。例えば `=>`、`>=`、`!=`、`===` のような
> コードが `⇒`、`≥`、`≠`、`≡` のようにより読みやすい記号で表示されます。コードの意味を視覚的により明確にします。

### ターミナルフォント設定

Editor → Color Scheme → Console Font で次のように設定します：

- 「Use console font instead of the default」をチェック
- Font: **D2CodingLigature Nerd Font**
- Size: **14**
- Line height: **1.2**

### ターミナル追加設定

Tools → Terminal で次のように設定します：

- Shell path: `/bin/zsh`（macOS のデフォルト値なので通常すでに設定済み）
- Environment variables: `TERM=xterm-256color` 追加

> [!INFO]
> **設定項目説明**
>
> **Shell path**: macOS は基本的に zsh を使用するので `/bin/zsh` がすでに設定されています。Oh My Zsh インストールの有無に関係なく同じです。
>
> **Environment variables - TERM**: ターミナルの色サポートレベルを定義します。`xterm-256color` に設定すると 256 色をサポートして
> ターミナルテーマの色が正しく表示されます。特に Powerlevel10k のようなテーマで重要です。

## ターミナルからプロジェクトを開く

### Shell Script 有効化

まず JetBrains Toolbox で shell script を有効化する必要があります：

1. **JetBrains Toolbox** を開く
2. 右上の**設定**アイコンをクリック（⚙️）
3. **Settings** → **Tools** タブ
4. **Generate shell scripts** をチェック
5. **Shell scripts location** パスを確認（通常 `/usr/local/bin`）

> [!INFO]
> **Shell Script とは何か？**
>
> Shell Script はターミナルから `idea .` のようなコマンドで IDE を実行できるようにする実行ファイルです。
> JetBrains Toolbox が自動的に生成してくれ、インストールされたすべての JetBrains IDE に対してコマンドを作成します。

設定完了後、ターミナルから IntelliJ を直接実行できます。

現在位置のプロジェクトを IntelliJ で開くには、ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
# 現在のディレクトリを IntelliJ で開く
idea .
```

特定パスのプロジェクトを開くには、ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
# 特定のプロジェクトを開く
idea ~/projects/my-project
```

[戻る](macos-step01-essential-developer-tools)
