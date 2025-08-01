---
title: Windowsでの韓国語と英語の切り替えキーの変更
description: Windows 11で、1つのキーボードでMacとWindowsを同時に使用する環境にいるため、韓国語と英語の切り替えに不便を感じました。\
authors:
  - XIYO
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:57:19+09:00
---
# Windowsでの韓国語と英語の切り替えキーの変更

Windows 11で、1つのキーボードでMacとWindowsを同時に使用する環境にいるため、韓国語と英語の切り替えに不便を感じました。\
どのキーで韓国語と英語を切り替えるか悩んだ結果、Macの韓国語と英語の切り替えに従うことに決めました。

## キーの変更

### オペレーティングシステムの内蔵機能を利用

Windowsの内蔵機能を利用しつつ、Macと同様に<kbd>shift</kbd> + <kbd>space</kbd>キーで韓国語と英語を切り替えることにしました。

#### キーボードレイアウトの変更

1. <kbd>win</kbd> + <kbd>i</kbd>キーを押して設定画面を開きます。
2. メニューから「時間と言語」ボタンをクリックします。
3. メインエリアで「言語と地域」ボタンをクリックします。
4. メインエリアの言語セクションで「韓国語」フィールドの「...」ボタンをクリックし、「言語オプション」ボタンをクリックします。
5. メインエリアのキーボードセクションで「レイアウト変更」ボタンをクリックします。
6. 「ハードウェアキーボードレイアウト変更ウィンドウ」で「韓国語キーボード（101キー）種類3」をクリックし、「今すぐ再起動」ボタンをクリックします。

#### レジストリの変更

Googleで「キーボード 韓英 レジストリ 変更」を検索すると、「キーボードレイアウト変更」をレジストリで行う方法が見つかります。（すでにUIを提供しているのに、なぜ？...）\
説明は実際のキーのマッピングを変更する最もよく説明されたリンクに置き換えます。この方法は手間がかかるため、お勧めしません。

[最もよく説明されたブログ](https://lightinglife.tistory.com/entry/%EC%9C%88%EB%8F%84%EC%9A%B0%EC%97%90%EC%84%9C-%EB%A7%A5%EC%B2%98%EB%9F%BC-Capslock%EC%BA%A1%EC%8A%A4%EB%9D%BD%ED%82%A4%EB%A5%BC-%ED%95%9C%EC%98%81%ED%82%A4%EB%A1%9C-%EB%B3%80%EA%B2%BD%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95by-%EB%A0%88%EC%A7%80%EC%8A%A4%ED%8A%B8%EB%A6%AC-%ED%8E%B8%EC%A7%91#google_vignette)

### ユーティリティプログラムを利用

#### PowerToys

この場合、<kbd>win</kbd> + <kbd>space</kbd>キーで韓国語と英語を切り替えることにしました。

1. Microsoft Storeから[PowerToys](https://apps.microsoft.com/store/detail/XP89DCGQ3K6VLD?ocid=pdpshare)をインストールします。
2. PowerToysアプリを起動し、「メニュー」エリアで「キーボードマネージャ」ボタンをクリックします。
3. 「メイン」エリアの「ショートカットの再マッピング」ボタンをクリックします。
   ![キーボードマネージャエリアでのショートカットの再マッピング](./assets/changing-the-korean-english-switch-key-20240918110239147.png)
4. 「ショートカットの再マッピング」ウィンドウでキーをマッピングします。
   1. 「選択」エリアでウィンドウの「ショートカット」横の✏️ボタンをクリックし、組み合わせキーを入力します。
      ![Windowsキーとスペースの組み合わせキーを韓国語と英語に使用](./assets/changing-the-korean-english-switch-key-20240918110408909.png)
   2. 「対象」エリアでも同様に「ショートカット」横の✏️ボタンをクリックし、「韓国語と英語」キーを入力します。
5. 「ショートカットの再マッピング」ウィンドウで「保存」ボタンをクリックします。
6. 「キーボードマネージャ」ウィンドウで「適用」ボタンをクリックします。
   ![韓国語と英語キーが追加で登録された状態](./assets/changing-the-korean-english-switch-key-20240918110510904.png)

これで韓国語と英語の切り替えは2つの方法で可能です。

#### バダヤクのjwShiftSpaceKey

[公式ホームページ](https://badayak.com/entry/WinHanEng-jwShiftSpaceKey)

この部分は特に説明しません... 😘

