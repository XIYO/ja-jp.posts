---
title: Git Hooksによるマークダウンフロントマター自動化への道のり
authors:
  - XIYO
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T02:44:45+09:00
---
# Git Hooksによるマークダウンフロントマター自動化への道のり

## 序: 問題の始まり - Pre-commit Hookの限界

マークダウンブログを運営しながら、各投稿のフロントマターを手動で管理するのは面倒でした。特にコミットメッセージ、作成者、日付などのメタデータを毎回直接入力しなければならない状況でした。

最初は**pre-commit hook**を使って解決しようとしました。

```bash
# .husky/pre-commit (初期バージョン)
# ステージングされたマークダウンファイルのフロントマター更新
```

### Pre-commit方式の問題点

しかし、すぐに深刻な問題を発見しました：

1. **ステージング変更の残存**: フロントマターを更新すると、常にGitステージに新しい変更が残る
2. **追加コミットが必要**: 更新されたフロントマターを反映するために、別のコミットが必要
3. **コミットメッセージへのアクセス不可**: 最も致命的なことに、pre-commitの段階ではまだコミットメッセージが確定していないため、フロントマターに含めることができない

```javascript
// pre-commitではこれは不可能
const commitMessage = "???"; // まだ存在しない
```

## 破: Post-commit Hookへの転換

Pre-commitの限界を悟り、**post-commit hook**へと方向を転換しました。

```bash
# .husky/post-commit
# コミット完了後、フロントマター更新 + git commit --amend
```

### Post-commit + Amend方式

この方式は次のように動作しました：

1. ユーザーがコミット: `"✨ 新機能追加"`
2. Post-commit hook実行
3. コミット履歴からメッセージを抽出し、フロントマターを更新
4. `git commit --amend --no-edit --no-verify`で既存のコミットに変更を含める

```javascript
// scripts/update-frontmatter-postcommit.js
const changedFiles = execSync('git diff --name-only HEAD HEAD~1')
  .trim().split('\n').filter(file => file.endsWith('.md'));

// ... フロントマター更新 ...

// 既存のコミットに変更を追加
execSync('git commit --amend --no-edit --no-verify');
```

### 新たな複雑性の出現

Post-commit方式はコミットメッセージアクセスの問題を解決しましたが、新しい問題が生じました：

1. **無限ループのリスク**: `git commit --amend`が別のpost-commit hookをトリガー
2. **複雑な防止ロジックが必要**:
   ```bash
   # 無限ループ防止コード
   if [ "$FRONTMATTER_UPDATE_RUNNING" = "1" ]; then
     exit 0
   fi
   export FRONTMATTER_UPDATE_RUNNING=1
   ```
3. **Git履歴の改ざん**: SHA変更によるコラボレーション時の衝突の可能性
4. **--no-verifyの限界**: Post-commit hookは`--no-verify`でスキップできないことを発見

## 急: 根本的な解決策の探求

複雑になったコードを見て、もっと良い方法があるはずだと思いました。Git hooksについてより深く調査した結果、**prepare-commit-msg hook**という完璧な解決策を発見しました。

### prepare-commit-msg Hookの発見

ウェブ検索を通じて、Gitコミットワークフローの正確な順序を確認しました：

1. ファイルのステージング (`git add`)
2. **pre-commit** hook実行
3. **prepare-commit-msg** hook実行 ← **ここが鍵！**
4. **commit-msg** hook実行
5. 実際のコミット作成
6. **post-commit** hook実行

### Prepare-commit-msgの完璧なタイミング

このhookの特徴を発見しました：

- ✅ コミットメッセージはすでに確定済み
- ✅ まだコミットが作成される前
- ✅ ファイル修正後の再ステージングが可能
- ✅ 同じコミットに自動的に含まれる

```bash
# prepare-commit-msg hookパラメータ
# $1 = コミットメッセージファイルパス
# $2 = コミットソース (message, template, merge など)

CURRENT_MSG=$(cat "$1")  # コミットメッセージを読める！
```

## 結: 完璧な解決策の実装

### 最終的な実装

prepare-commit-msg方式で完全に再実装しました：

```bash
# .husky/prepare-commit-msg
#!/bin/sh

COMMIT_MSG_FILE="$1"
COMMIT_SOURCE="$2"

# 通常のコミットでのみ実行
if [ "$COMMIT_SOURCE" = "message" ] || [ -z "$COMMIT_SOURCE" ]; then
  CURRENT_MSG=$(cat "$COMMIT_MSG_FILE")
  
  # ステージングされたマークダウンファイルを検索
  STAGED_MD_FILES=$(git diff --cached --name-only --diff-filter=ACM | grep '\.md$')
  
  if [ -n "$STAGED_MD_FILES" ]; then
    export COMMIT_MESSAGE="$CURRENT_MSG"
    
    if pnpm exec node scripts/update-frontmatter-prepare.js; then
      echo "✅ フロントマターが正常に更新され、再ステージングされました"
    fi
  fi
fi
```

```javascript
// scripts/update-frontmatter-prepare.js
const commitMessage = process.env.COMMIT_MESSAGE;
const stagedFiles = execSync('git diff --cached --name-only --diff-filter=ACM')
  .trim().split('\n').filter(file => file && file.endsWith('.md'));

// フロントマター更新
const updatedData = {
  title: title,
  description: description,
  authors: uniqueAuthors,
  dates: dates,
  messages: [commitMessage, ...existingMessages], // 現在のコミットメッセージを含む！
  created: createdDate,
  modified: modifiedDate
};

// ファイル更新後、自動再ステージング
writeFileSync(filePath, updatedContent);
execSync(`git add "${file}"`); // 自動的に同じコミットに含まれる
```

### 革新的な結果

最終実装の利点：

1. **完璧なタイミング**: コミットメッセージ確定後、コミット作成前
2. **自動包含**: 再ステージングされた変更が自然に同じコミットに含まれる
3. **複雑性の除去**: 無限ループ防止ロジックが不要
4. **履歴の整合性**: SHA変更なし、amendが不要
5. **コラボレーションの安全性**: Gitの正当なワークフローを活用

### 実際の動作例

```bash
$ git commit -m "✨ 新機能追加"

🔍 pre-commitチェックを実行中...
✅ すべてのpre-commitチェックに合格しました！

📝 prepare-commit-msg hookを実行中...
📄 ステージングされたマークダウンファイルを発見: new-feature.md
✅ new-feature.md のフロントマター更新完了
✅ 更新されたフロントマターがステージングされました。

📝 コミットメッセージを検証中...
✅ コミットメッセージの検証に合格

[main abc1234] ✨ 新機能追加
 2 files changed, 50 insertions(+)
```

生成されたマークダウン：

```yaml
---
title: 新機能
description: 今回追加した革新的な機能です
authors:
  - XIYO
messages:
  - '✨ 新機能追加'  # 自動的に含まれる！
created: '2025-07-20T09:40:48.024Z'
modified: '2025-07-20T09:40:48.024Z'
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T02:44:45+09:00
---

# 新機能

今回追加した革新的な機能です...
```

## 結論: 正しいツールを見つける旅

このプロジェクトから学んだ教訓：

1. **問題の根本的な理解**: 単に動作する解決策ではなく、なぜその問題が発生するのかを理解する
2. **ツールの深い探求**: Git hooksの様々な種類とそれぞれの特性を把握する
3. **複雑性はシグナル**: コードが複雑になった場合、より良い方法がある可能性がある
4. **正当な方法の力**: Gitの設計意図に合ったワークフローを活用する

Pre-commit → Post-commit → Prepare-commit-msgへと続いたこの旅は、単なる技術的な解決策を超えて、問題解決の本質について考えさせられる貴重な経験でした。

---

*この投稿のフロントマターもprepare-commit-msg hookによって自動生成されました！🎉*
