---
title: "Obsidian同期設定"
description: "マルチデバイスアクセスのためのGit、iCloud、またはObsidian Syncの設定"
authors:
  - XIYO
dates:
  - Thu Jul 17 2025 09:00:00 GMT+0900 (대한민국 표준시)
tags: obsidian, sync, git, cloud, backup
---

# Obsidian同期設定

> [!NOTE]
> **複数のデバイスでノートを同期する**
> デスクトップ、ノートパソコン、モバイル、タブレットで同じノートを使用する方法です。

## 同期オプションの比較

| 方法 | 価格 | デスクトップ | モバイル | リアルタイム | バージョン管理 |
|------|------|------------|----------|------------|--------------|
| Obsidian Sync | $4/月 | O | O | O | O |
| Git (Obsidian Git) | 無料 | O | X | 自動 | O |
| iCloud | 無料 | O | O | O | X |
| **Git + iCloud** | 無料 | O | O | O | O |

## Git同期（開発者推奨）

> [!IMPORTANT]
> **事前準備が必要**
> GitとGitHubの設定が必要です。[Git & GitHub設定ガイド](../mac-setup/git-github-setup)を先に完了してください。

### Obsidian Gitプラグインのインストール

1. 設定 → Community plugins → Browse
2. 「Obsidian Git」を検索してインストール
3. プラグインを有効化

### Gitリポジトリの初期化

ターミナルを開いて以下のコマンドをコピー＆ペースト：
```bash
cd ~/Documents/Obsidian/YourVault
git init
echo ".obsidian/workspace*" >> .gitignore
git add .
git commit -m "Initial commit"
```

### GitHubリポジトリの接続

> [!TIP]
> **ghで既にログインしている場合**
> GitHub CLIでログインしていれば、認証は自動的に処理されます。

ターミナルを開いて以下のコマンドをコピー＆ペースト：
```bash
gh repo create obsidian-vault --private --source=. --remote=origin --push
```

### Obsidian Gitプラグインの設定

設定 → Obsidian Gitで：

#### 基本設定
- **Vault backup interval**：10（10分ごとに自動バックアップ）
- **Auto pull interval**：10（10分ごとに自動プル）
- **Commit message**：`vault backup: {{date}}`
- **Pull updates on startup**：ON（起動時に最新バージョンを取得）
- **Push on backup**：ON（バックアップ時に自動プッシュ）

#### 詳細設定
- **Sync method**：Merge（競合時にマージ）
- **Pull method**：Merge（プル時のマージ方式）
- **Disable push**：OFF（プッシュ有効化）
- **Disable notifications**：OFF（通知表示）
- **Show status bar**：ON（ステータスバーにGitステータス表示）

#### 自動バックアップトリガー
- **Backup on file save**：ON（ファイル保存時にバックアップ）
- **Backup after file change**：ON（ファイル変更後にバックアップ）
- **Auto backup after latest commit**：5（最後のコミットから5分後に自動バックアップ）

> [!IMPORTANT]
> **アプリ終了時の自動バックアップ**
> Obsidianを終了またはスリープモード移行時に自動バックアップするには：
> 1. **コマンドパレット**（Cmd+P） → 「Obsidian Git: Create backup」をホットキーに登録
> 2. **macOSショートカットアプリ**で自動化を作成：
>    - トリガー：「アプリが終了する時」または「スリープモード移行時」
>    - アクション：Obsidian Git backupを実行
>
> またはより簡単に：
> - **Auto backup after latest commit**：1〜2分に設定
> - これで最後の変更後1-2分以内に常にバックアップされます。

#### ファイル管理
- **List of files to not commit**：
  ```
  .obsidian/workspace*
  .obsidian/app.json
  .obsidian/appearance.json
  .trash/
  .DS_Store
  ```
- **Pull changes before push**：ON（プッシュ前にプル実行）

#### パフォーマンス最適化
- **Improved performance for large vaults**：ON（大きなVaultの最適化）
- **Show changes files count**：ON（変更ファイル数表示）

> [!TIP]
> **コミットメッセージ変数**
> - `{{date}}`：現在の日付/時刻
> - `{{hostname}}`：コンピュータ名
> - `{{numFiles}}`：変更されたファイル数
>
> 例：`vault backup: {{date}} on {{hostname}} ({{numFiles}} files)`

> [!INFO]
> **設定完了**
>
> これで自動的にGitにバックアップされます。
> 別途の認証設定なしでghクレデンシャルを使用します。

## iCloud同期（Appleユーザー）

> [!IMPORTANT]
> **iPhoneで最初にVaultを作成する必要があります**
> iCloud DriveにObsidianディレクトリを作るには、必ずiPhoneのObsidianアプリで最初にVaultを作成する必要があります。Macでは直接作成できません。

### iPhoneでVaultを作成
1. **iPhoneでObsidianアプリをインストール**
2. **アプリを起動して「Create new vault」を選択**
3. **「Store in iCloud」オプションを選択**
4. **Vault名を指定**（例：MyVault）
5. **iCloud DriveにObsidianフォルダが自動作成される**

### Macで接続
1. **Finderを開く** → **iCloud Drive**
2. **Obsidianフォルダ**を探す
3. **Mac Obsidianで「Open folder as vault」を選択**
4. **iCloud Drive → Obsidian → MyVaultを選択**

### 利点
- 設定が非常に簡単
- リアルタイム同期
- すべてのAppleデバイスサポート

### 欠点
- Appleデバイスのみ可能
- バージョン管理なし
- iPhoneで最初に設定が必要

## Obsidian Sync（公式ソリューション）

### 利点
- すべてのプラットフォームサポート
- エンドツーエンド暗号化
- バージョン履歴

### 価格
- **$4/月**（年間請求）
- 学生40%割引：[申請はこちら](https://obsidian.md/student-discount)

### 設定
1. 設定 → Sync → Log in
2. サブスクリプション後自動同期

## ハイブリッド：Git + iCloud（最適なソリューション）

> [!TIP]
> **両方の方法の利点を活用**
> デスクトップではGitでバージョン管理、モバイルではiCloudでアクセス

### 設定方法

> [!WARNING]
> **順序が重要です！**
> 必ずiPhoneのObsidianアプリで最初にVaultを作成してiCloud DriveにObsidianディレクトリが作られるようにしてください。

1. **iPhoneでVaultを作成したか確認**
   - iPhone Obsidianアプリで「Store in iCloud」でVault作成
   - このプロセスがiCloud DriveにObsidianフォルダを自動作成

2. **MacでそのVaultを開く**
   ```
   ~/Library/Mobile Documents/com~apple~CloudDocs/Obsidian/MyVault
   ```

3. **Git初期化（上記のGit同期方法参照）**

4. **作業フロー**
   - デスクトップ：Gitでコミット/プッシュ（バージョン管理）
   - モバイル：iCloudで読み書き（リアルタイム同期）
   - Obsidian Gitプラグインが自動的に同期

### 利点
- すべてのデバイスで使用可能
- バージョン管理＋リアルタイム同期
- 完全無料

## 推奨事項

- **開発者**：Git + iCloudハイブリッド
- **一般ユーザー**：iCloud（Mac）またはObsidian Sync
- **クロスプラットフォーム**：Obsidian Sync

> [!WARNING]
> Git + iCloudハイブリッドは一度に1つのデバイスでのみ編集してください。同時編集時に競合の可能性があります。

## 次のステップ

同期設定が完了したら：
<!-- 
- [必須プラグインのインストール](step-02)
- [高度な設定](step-03)
-->