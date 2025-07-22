---
title: "Obsidian設定ガイド"
description: "効率的なノート作成のためのObsidianの必須設定と構成"
authors:
  - XIYO
dates:
  - Thu Jul 17 2025 09:00:00 GMT+0900 (대한민국 표준시)
tags: obsidian, settings, essential, first-setup
---

# Obsidian設定ガイド

Obsidianはマークダウンベースの強力なノートアプリです。ローカルファイルとして保存され、永続的に所有でき、リンクとグラフビューを通じて知識を結び付けて管理できます。開発ドキュメント、学習ノート、アイデアを体系的に整理するのに最適化されています。

### Notionとの主な違い

| 特徴 | Obsidian | Notion |
|------|----------|--------|
| **データ保存** | ローカルマークダウンファイル | クラウド専用 |
| **速度** | 非常に高速（ローカル） | インターネット速度に依存 |
| **オフライン使用** | 完全サポート | 制限的 |
| **ファイル所有権** | 100%ユーザー所有 | サービス依存 |
| **カスタマイズ** | プラグインで無限拡張 | 制限されたブロックベース |
| **価格** | 無料（同期のみ有料） | 無料制限、有料必須 |
| **学習曲線** | 初期設定が必要 | すぐに使用可能 |

Obsidianは開発者や長期的な知識管理が必要なユーザーに適しており、データを完全に制御したい場合に最良の選択です。

## Obsidian初期設定

### 初回起動とVault作成
1. Obsidianを起動
2. 「Create new vault」を選択
3. Vault名を入力（例：「Dev Notes」、「Knowledge Base」）
4. 保存場所を選択

> [!WARNING]
> **必ず最初に設定してください**
> 後で変更すると既存のノートを修正する必要があるかもしれません。

## 必須設定

### マークダウンリンクを使用（WikiリンクOFF）

設定（Cmd+,） → Files & Links：
- **Use `Wikilinks`**：OFF
- **Relative path to file**：ON

> [!INFO]
> Wikiリンク `[[ファイル名]]` の代わりに標準マークダウン `[テキスト](ファイル名)` を使用します。
> GitHub、VS Codeなど他のマークダウンエディタと互換性があります。

### 添付ファイルの整理（assetsフォルダ）

設定 → Files & Links：
- **Default location for new attachments**：「In the folder specified below」
- **Attachment folder path**：`assets`

画像やファイルをドラッグすると：
```
[DIR] Vault ルート/
  [DIR] assets/        ← すべての添付ファイルがここに
    [IMG] image1.png
    [IMG] image2.png
  [DIR] notes/
    [FILE] ノート1.md
    [FILE] ノート2.md
```

> [!INFO]
> **リンクの自動更新**：Automatically update internal linksをONに設定すると、ファイル名が変更されたときにリンクも自動的に更新されます。

### 画面全体を使用

設定 → Editor：
- **Readable line length**：OFF

狭い領域ではなく画面全体を使用して文章を作成できます。

## 追加推奨設定

### 外観設定
設定 → Appearanceで：
- **Base theme**：Dark/Light（お好みで）
- **Translucent window**：ON（Macできれい）

### 自動保存
設定 → Editorで：
- **Autosave after delay**：2（2秒後に自動保存）

### エディタ設定
設定 → Editorで：
- **Show line numbers**：ON（コード作成時に便利）
- **Show frontmatter**：ON（メタデータ表示）
- **Fold heading**：ON（長いドキュメント管理）
- **Fold indent**：ON（インデント折りたたみ）
- **Tab size**：2または4（コードスタイルに合わせて）
- **Use tabs**：OFF（スペース使用推奨）

### ファイルとフォルダ設定
設定 → Files & Linksで：
- **Excluded files**：
  ```
  .DS_Store
  .git/
  node_modules/
  ```

### 新規ファイルテンプレート
設定 → Core plugins → Templates有効化後：
1. テンプレートフォルダの場所を指定
2. デフォルトテンプレートファイルを作成

## 設定確認

新しいノートを作成してテスト：

1. **リンクテスト**：
   - `Cmd + K`でリンク作成 → `[](test)` 形式か確認

2. **画像テスト**：
   - 画像をドラッグ → `assets` フォルダに保存されるか確認

3. **画面テスト**：
   - 長い文章を入力 → 画面端までテキストが表示されるか確認

> [!INFO]
> **設定完了**
>
> これでObsidianを効率的に使用する準備ができました。

## 必須ショートカット＆基本機能の有効化

### コアショートカット（必ず覚えるべきもの）
- `Cmd + P`：**コマンドパレット**（すべてのコマンドを実行）
- `Cmd + O`：**クイックスイッチャー**（ファイル検索と開く）
- `Cmd + N`：新規ノート作成
- `Cmd + Shift + N`：新規ノート作成（新しいウィンドウで）
- `Cmd + W`：現在のタブを閉じる
- `Cmd + Shift + F`：Vault全体を検索
- `Cmd + F`：現在のノートで検索
- `Cmd + E`：編集/読み取りモード切り替え
- `Cmd + K`：リンク挿入
- `Cmd + B`：**太字**
- `Cmd + I`：*斜体*

### 隠れた基本機能の有効化

#### 録音機能の有効化
設定 → Core plugins → **Audio recorder** 有効化

使用方法：
- 録音開始：左サイドバーのマイクアイコンをクリック
- ホットキー設定：設定 → Hotkeys → 「Start/stop recording」を検索
- 推奨ホットキー：`Cmd + Shift + R`
- 録音ファイルは自動的にassetsフォルダに保存

#### スライドプレゼンテーション
設定 → Core plugins → **Slides** 有効化

使用方法：
- ノートに `---` でスライドを区切る
- コマンドパレット → 「Start presentation」を実行
- プレゼンテーションモードに切り替え

#### キャンバス（無限ホワイトボード）
設定 → Core plugins → **Canvas** 有効化

使用方法：
- `Cmd + N` → ファイル形式で「Canvas」を選択
- ノート、画像、リンクを視覚的に接続
- マインドマップ、フローチャート作成可能

#### デイリーノート
設定 → Core plugins → **Daily notes** 有効化

設定：
- Date format：`YYYY-MM-DD`
- New file location：`daily/`（フォルダ自動作成）
- Template file location：テンプレート設定可能

### パワーユーザーショートカット
- `Cmd + P` 後 `>`：コマンドのみ表示
- `Cmd + P` 後 `#`：タグ検索
- `Cmd + P` 後 `^`：見出し検索
- `Cmd + [` / `Cmd + ]`：戻る/進む
- `Option + Enter`：リンクを新しいウィンドウで開く
- `Cmd + Option + ←/→`：タブ移動
- `Cmd + \`：サイドバー切り替え

### カスタムホットキー必須設定
設定 → Hotkeysで追加：
- **Toggle left sidebar**：`Cmd + 1`
- **Toggle right sidebar**：`Cmd + 2`
- **Focus on editor**：`Cmd + 0`
- **Move line up/down**：`Option + ↑/↓`
- **Delete paragraph**：`Cmd + D`
- **Open in default app**：`Cmd + Option + O`

## ノート作成のヒント

### リンクの活用（マークダウン形式）
- `[ノート名](ノート名)`：他のノートへのリンク
- `[セクションリンク](ノート名#見出し)`：特定のセクションへのリンク

### タグシステム
- `#project/frontend`：階層的タグの使用
- `#todo`、`#idea`、`#bug`：ステータス管理
- タグパネルで一目で確認

### デイリーノートの活用
毎朝デイリーノートを作成して：
- やることリストを作成
- 学習した内容を整理
- アイデアをメモ

## 次のステップ

基本設定が完了したら：
- [マークダウン基本機能](markdown-basics) - Mermaid、LaTeX、Calloutなど
- [同期設定](obsidian-step01-sync-settings) - Git、Cloud、Obsidian Sync