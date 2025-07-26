---
title: INTELLIJでの強制プッシュの有効化
description: IntelliJでは、マスターやメインブランチに対して強制プッシュが基本的に保護されています。 \
dates:
  - "2025-07-21T16:57:19.000Z"
  - "2025-07-21T16:33:12.000Z"
  - "2025-06-15T06:10:59.000Z"
  - "2024-09-18T02:16:48.000Z"
  - "2024-09-08T03:40:36.000Z"
  - "2024-09-07T10:43:12.000Z"
authors:
  - XIYO
---
# INTELLIJでの強制プッシュの有効化

IntelliJでは、マスターやメインブランチに対して強制プッシュが基本的に保護されています。 \
これを解決する方法を見ていきましょう。

## シナリオ

GitHub Actionsを使用して自動デプロイを行うために、いくつかの文法エラーに遭遇しました。 \
そのため、コミットログに残った雑多なテストコードを整理するために、強制プッシュを有効にする必要がありました。

## 解決策

!["search everywhere" を開く](./assets/enable-force-push-20240918104825841.png)
!["protected branch" フィールドを修正](./assets/enable-force-push-20240918104833418.png)

- 方法 0. <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>A</kbd> の組み合わせショートカットを入力して `Search Everywhere` ウィンドウを開きます。  
0. `Search Everywhere` ウィンドウで「Protected branches:」と入力し、一致する項目をクリックします。  
0. `settings` ウィンドウで `Protected branches:` フィールドを見つけ、内容を削除します。

## トラブルシューティング

GitHubとGitLabにはブランチ保護機能があるため、各リポジトリの設定を確認する必要があります。

