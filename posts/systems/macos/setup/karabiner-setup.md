---
title: Karabiner-Elements 設定ガイド
description: >-
  Karabiner-Elements は macOS のキーボード動作を自由にカスタマイズできる強力なツールです。このガイドでは最も便利な 3
  つの設定を扱います。
authors:
  - XIYO
tags:
  - mac-setup
  - karabiner
  - keyboard
  - productivity
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T02:44:45+09:00
---

# Karabiner-Elements 設定ガイド

Karabiner-Elements は macOS のキーボード動作を自由にカスタマイズできる強力なツールです。このガイドでは最も便利な 3 つの設定を扱います。

## Karabiner-Elements のインストール

ターミナルを開いて Homebrew でインストールします：

```bash
brew install --cask karabiner-elements
```

インストール後、システム権限を許可する必要があります：
1. システム設定 → プライバシーとセキュリティ
2. 入力監視で Karabiner 関連項目をすべて許可

## 基本設定：韓英切り替えの改善

### 右 Command を韓英キーに変更

macOS のデフォルト韓英切り替え（Caps Lock）には遅延があって不便です。右 Command キーを韓英切り替えに変えてみましょう。

Karabiner-Elements を実行して次のように設定します：

1. **Simple Modifications** タブをクリック
2. **Add item** ボタンをクリック
3. From key: `right_command` → To key: `f18` を選択

macOS キーボード設定で韓英切り替えショートカットを変更します：

1. システム設定 → キーボード → ショートカット → 入力ソース
2. 「入力メニューで次のソースを選択」をクリック
3. 右 Command キーを押す（F18 として認識される）

これで右 Command キーで即座に韓英切り替えが可能です。

## Ultimate macOS のインストール

Ultimate macOS は数十種類の便利なキーボード設定が含まれた総合パッケージです。一度インストールすれば必要な機能だけを選んで有効化できます。

### インストール方法

1. Karabiner-Elements を実行
2. **Complex Modifications** タブに移動
3. **Add rule** ボタンをクリック
4. **Import more rules from the Internet** をクリック
5. 検索窓に **"ultimate macOS"** を入力
6. **"ultimate macOS"** by suliveevil を選択して **Import**

### Vim スタイル方向キー設定（hjkl）

Ultimate macOS をインストールしたら、様々な Vim 関連設定を使用できます。

#### Vi Mode を有効化する

1. Complex Modifications で Ultimate macOS ルールリストを確認
2. 次のいずれかを選択して **Enable**：
   - **"Vi Mode [Hold ⇪ Caps Lock for Vi Mode]"**: Caps Lock を押している間だけ hjkl が方向キーとして動作
   - **"Vi Mode [⌃ Control + hjkl]"**: Control + hjkl で方向キー使用
   - **"Vi Mode [fn + hjkl]"**: fn + hjkl で方向キー使用

> [!TIP]
> **おすすめ設定**
> 
> "Hold ⇪ Caps Lock for Vi Mode" が最も実用的です。
> Caps Lock を押した状態でのみ動作するため、通常のタイピングに邪魔になりません。

#### 使用可能なショートカット

Vi Mode を有効化すると次の機能を使用できます：

- **基本移動**
  - h: ← （左）
  - j: ↓ （下）
  - k: ↑ （上）
  - l: → （右）

- **拡張移動**（一部モードで対応）
  - w: 次の単語に移動
  - b: 前の単語に移動
  - 0: 行の先頭へ
  - $: 行の末尾へ

### その他の便利な機能

Ultimate macOS には次のような便利な機能も含まれています：

#### Hyper Key 設定
"⇪ Caps Lock → Hyper Key (⌃⌥⇧⌘)" を有効化：
- Caps Lock を特別な modifier キーに変更
- 他のアプリと衝突しない固有のショートカット作成可能

#### 韓国語ユーザー向け設定
"Korean" カテゴリで：
- **"⇧ Shift + Space → Switch Input Source"**: Shift+Space で韓英切り替え
- **"₩ → ` or ₩ (Hold ⌥ Option)"**: ウォンキーをバックティックに変更

#### 開発者向け設定
- **"⎋ Escape → ` ~ (Hold ⇧ Shift)"**: ESC キーでバックティック入力
- **"Delete Line/Word"**: 高速削除ショートカット
- **"Emacs Mode"**: Emacs スタイルショートカット（Control+A/E など）

## 使用のヒント

### 設定のバックアップ
設定をバックアップするには次のファイルを保存してください：
```bash
~/.config/karabiner/karabiner.json
```

### トラブルシューティング
- 設定が動作しない場合は Karabiner-Elements を再起動してください
- システム設定で権限が正しく付与されているか確認してください
- 他のキーボードユーティリティと衝突する可能性があるので注意してください

### 元に戻す
1. Complex Modifications で有効化したルールを **Remove**
2. Simple Modifications で設定を削除
3. 必要に応じて Karabiner-Elements を削除：
   ```bash
   brew uninstall --cask karabiner-elements
   ```

> [!TIP]
> **段階的アプローチ**
> 
> 1. まず韓英切り替え改善だけ使ってみてください
> 2. Ultimate macOS インストール後、Vi Mode だけ有効化してみてください
> 3. 慣れたらより多くの機能を一つずつ追加してください

これでキーボードを 200% 活用できます！
