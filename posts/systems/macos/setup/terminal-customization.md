---
title: ターミナルカスタマイズガイド
authors:
  - XIYO
tags:
  - mac-setup
  - terminal
  - oh-my-zsh
  - powerlevel10k
  - iterm2
  - zsh
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T02:44:45+09:00
---

# ターミナルカスタマイズガイド

> [!NOTE]
> **事前要件**
> [開発者必須ツールのインストール](macos-step01-essential-developer-tools)が完了している必要があります。

## Oh My Zsh とは？

Oh My Zsh はターミナルをより美しく便利にするツールです。
コマンドを入力する時に自動補完され、色で区別して表示し、Git 情報も一目で見えるようにします。

> [!INFO]
> **Oh My Zsh が提供する機能**
> 
> - **テーマ**: ターミナルの見た目と色を変更します
> - **プラグイン**: 自動補完、構文強調などの便利機能を追加します
> - **エイリアス**: 長いコマンドを短く使えるようにします
> - **Git 情報**: 現在のブランチと状態をプロンプトに表示します

## Oh My Zsh のインストール

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

インストール中に表示される質問には **Y** を入力してください：

- "Do you want to change your default shell to zsh?" → **Y** を入力

> [!INFO]
> **インストール後に自動的に起こること**
> 
> 1. 既存の `.zshrc` ファイルが `.zshrc.pre-oh-my-zsh` にバックアップされます
> 2. 新しい `.zshrc` ファイルが生成されて Oh My Zsh が有効化されます
> 3. デフォルトテーマが適用されてターミナルの見た目が変わります

## テーマとプラグインのインストール

Oh My Zsh がインストールされたら、より素敵なテーマと便利なプラグインをインストールしてみましょう。

### インストールするコンポーネント

- **Powerlevel10k**: 最も人気のあるターミナルテーマ（速くて美しい）
- **zsh-autosuggestions**: 以前に入力したコマンドを灰色で事前表示
- **zsh-syntax-highlighting**: 正しいコマンドは緑色、間違ったコマンドは赤色で表示

### Powerlevel10k テーマのインストール

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### zsh-autosuggestions プラグインのインストール

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### zsh-syntax-highlighting プラグインのインストール

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 設定ファイルの更新

インストールしたテーマとプラグインを有効化するために設定を更新します：

```bash
# テーマ変更
sed -i '' 's/ZSH_THEME=".*"/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc

# プラグイン有効化 
sed -i '' 's/plugins=(.*)/plugins=(git docker docker-compose zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc

# 設定適用
source ~/.zshrc
```

> [!INFO]
> **有効化されるプラグイン**
> 
> - **git**: Git 関連のエイリアスと情報表示
> - **docker**: Docker コマンド自動補完
> - **docker-compose**: Docker Compose 自動補完
> - **zsh-autosuggestions**: コマンド提案機能
> - **zsh-syntax-highlighting**: コマンド構文強調


## iTerm2 カラーテーマの変更

ターミナルをもっときれいにしたいならカラーテーマを変えてみましょう。

> [!INFO]
> **カラーテーマとは？**
> 
> ターミナルの背景色、文字色、強調色などを全体的に変える色の組み合わせです。
> iTerm2 には基本的に提供されるテーマがあり、追加でダウンロードすることもできます。

### 基本提供テーマに変更する

まず iTerm2 に内蔵されたテーマを確認してみましょう：

1. **iTerm2 → Settings → Profiles → Colors**
2. 右下の **"Color Presets..."** ドロップダウンをクリック
3. 次のような基本テーマがあります：
   - **Dark Background**（基本ダークテーマ）
   - **Light Background**（明るいテーマ）
   - **Pastel (Dark Background)**（パステル系）
   - **Solarized Dark**（人気のあるダークテーマ）
   - **Solarized Light**（人気のある明るいテーマ）
   - **Tango Dark** / **Tango Light**
4. 希望のテーマをクリックして即座に適用

### より多くのテーマをインストール

基本テーマが気に入らない場合、数百種類の追加テーマをダウンロードできます。

#### 人気テーマのおすすめ

- **Dracula**: ダークパープル系の人気テーマ
- **Tokyo Night**: モダンなダークテーマ  
- **Gruvbox Dark**: 暖かい色感のレトロテーマ
- **Catppuccin**: パステルトーンの柔らかいテーマ
- **Nord**: 冷たいブルー系のミニマルテーマ

#### 追加テーマのダウンロードとインストール

1. [iTerm2 Color Schemes](https://iterm2colorschemes.com) ウェブサイトにアクセス
2. 気に入ったテーマのプレビューを確認
3. テーマ名リンクを**右クリック** → **「リンク先のファイルをダウンロード」**を選択して `.itermcolors` ファイルをダウンロード
4. iTerm2 に戻って：
   - **Settings → Profiles → Colors**
   - **"Color Presets..."** → **"Import..."** をクリック
   - ダウンロードした `.itermcolors` ファイルを選択
   - インポートしたテーマを **"Color Presets..."** から選択して適用

> [!INFO]
> **ダウンロードしたテーマファイルは削除可能**
> 
> iTerm2 にテーマを Import すると設定が複製されて保存されるので、
> ダウンロードフォルダにある `.itermcolors` ファイルは削除しても構いません。

> [!TIP]
> **テーマ選択のヒント**
> 
> - 長時間コーディングするならダークテーマが目に優しいです

## Powerlevel10k 設定ウィザード

ターミナルを再起動すると Powerlevel10k 設定ウィザードが自動的に開始されます。

### MesloLGS NF フォントインストール案内

設定ウィザード開始前に MesloLGS NF フォントインストールを勧める画面が表示されます：

> [!IMPORTANT]
> **Powerlevel10k フォントインストールプロセス**
> 
> 1. **"Install Meslo Nerd Font?"** 質問が表示されたら → **y** を入力
> 2. Powerlevel10k が自動的に MesloLGS NF フォントをダウンロードしてインストールします
> 3. **iTerm2 設定も自動的に変更されます**（フォントが MesloLGS NF に変わる）
> 
> このフォントは Powerlevel10k に最適化されていますが、韓国語がうまく表示されない場合があります。

### 設定ウィザードの進行

> [!INFO]
> **設定ウィザードとは？**
> 
> Powerlevel10k がいくつかの質問を通じてユーザーの好みに合うプロンプトスタイルを作成する機能です。
> アイコン対応の有無、色スタイル、情報表示方式などを選択できます。

### おすすめ設定（初心者向け）

各質問に次のように選択することを推奨します：

- **Diamond** → **y**（ダイヤモンドアイコンが見えたら y）
- **Lock** → **y**（錠前アイコンが見えたら y）  
- **Debian** → **y**（Debian ロゴが見えたら y）
- **Style** → **3 (Rainbow)**（最も人気のあるカラフルなスタイル）
- **Character Set** → **1 (Unicode)**（ユニコード文字使用）
- **Prompt Style** → **3 (Pure)**（きれいな 2 行スタイル）
- **Transient Prompt** → **n**（デフォルト値維持）
- **Instant Prompt** → **1 (Verbose)**（高速起動）

### 韓国語フォントに再変更

Powerlevel10k 設定が終わると iTerm2 フォントが MesloLGS NF に変わっているでしょう。
韓国語を正しく表示するには D2Coding Nerd Font に再度変更する必要があります：

1. **iTerm2 → Settings**（または `Cmd + ,`）
2. **Profiles → Text** タブ選択
3. **Font** セクションで現在 "MesloLGS NF" になっていることを確認
4. **Change Font** をクリック
5. **"D2CodingLigature Nerd Font"** を選択
6. サイズは **14pt** 推奨

> [!INFO]
> **なぜフォントを 2 回設定するのか？**
> 
> - **MesloLGS NF**: Powerlevel10k が推奨するフォントで、すべてのアイコンが完璧に表示されますが韓国語表示が最適化されていません
> - **D2Coding Nerd Font**: 韓国語と英文、アイコンをすべてよく表示する韓国開発者用フォントです
> 
> Powerlevel10k 設定中は MesloLGS NF を使用し、設定後に D2Coding に変えるのが最も良いです。

> [!TIP]
> 設定を間違えたり後で変更したい場合はいつでも再設定できます：
> 
> ```bash
> p10k configure
> ```

## インストール確認

すべてのインストールが正しく行われたか確認してみましょう。

ターミナルを開いて以下のコマンドをコピー＆ペーストしてください：

```bash
echo $ZSH_THEME  # powerlevel10k/powerlevel10k が出力されるべき
echo $SHELL      # /bin/zsh が出力されるべき
```

### 正常インストール確認ポイント

1. **ターミナルプロンプト**: Git ブランチ名、フォルダアイコンなどが表示される
2. **自動補完**: コマンド入力時に灰色の文字で提案が表示される  
3. **構文強調**: 正しいコマンドは緑色、間違ったコマンドは赤色
4. **アイコン**: Nerd Font アイコンが壊れずに正常表示

## 追加のヒント

### 便利な Oh My Zsh エイリアス

Oh My Zsh が提供する便利な短縮コマンド：

- `ll` - `ls -l`（詳細ファイルリスト）
- `la` - `ls -la`（隠しファイル含むリスト）
- `..` - `cd ..`（上位フォルダへ）
- `...` - `cd ../..`（2 段階上へ）
- `gst` - `git status`（Git 状態確認）
- `gaa` - `git add --all`（すべての変更を追加）
- `gcmsg` - `git commit -m`（メッセージ付きコミット）

### Powerlevel10k 高度な設定

より多くの設定が必要なら `~/.p10k.zsh` ファイルを編集できます：

```bash
# 設定ファイル編集
code ~/.p10k.zsh  # VS Code で開く
```

> 最初はそのまま基本設定で使用することを推奨します。 
> ターミナルに慣れてからカスタマイズしてみてください！

[戻る](macos-step01-essential-developer-tools)
