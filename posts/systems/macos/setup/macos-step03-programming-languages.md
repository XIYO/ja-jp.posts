---
title: プログラミング言語のインストール
authors:
  - XIYO
tags:
  - mac-setup
  - java
  - openjdk
  - macos-step03-programming-languages
  - intellij
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-23T00:41:04+09:00
---

# プログラミング言語のインストール

> [!NOTE]
> **事前要件**
> [Homebrew のインストール](macos-step00-homebrew-installation)が完了している必要があります。

## Java インストールについてのアドバイス

> [!INFO]
> **IntelliJ IDEA が JDK を自動管理します**
> IntelliJ IDEA はプロジェクトごとに必要な JDK をダウンロードして管理します。システム全体に Java をインストールしなくても IntelliJ が自動で処理するので、必要な場合以外はインストールを延期してください。

### いつシステムに Java をインストールすべきか？

次の場合のみシステム全体の Java が必要です：

- ターミナルで `java` コマンドを直接使用する時
- IntelliJ なしで Java アプリケーションを実行する時
- CI/CD パイプラインで Java が必要な時

## Java 21 OpenJDK のインストール方法

本当に必要なら Homebrew で簡単にインストールできます。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
(brew install openjdk@21 || true)
```

> [!IMPORTANT]
> **JAVA_HOME は設定しないでください**
> Homebrew が自動で PATH を管理します。昔のやり方のように `.zshrc` に `export JAVA_HOME=...` を追加する必要はありません。

## インストール確認

インストール後、Java が正しく動作するか確認してください。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
java --version
```

以下のようなメッセージが表示されれば成功です：

```text
openjdk 21.x.x 2024-xx-xx
OpenJDK Runtime Environment Homebrew (build 21.x.x)
OpenJDK 64-Bit Server VM Homebrew (build 21.x.x, mixed mode, sharing)
```

> [!TIP]
> IntelliJ IDEA はシステムにインストールされた JDK を自動認識します。プロジェクト作成時にリストから選択すればOKです。

## 次のステップ

必要なツールがすべて準備できました！macOS をより効率的に使うためのヒントを学びましょう。

[次のステップ：macOS 便利技集](macos-step04-advanced-configurations)
