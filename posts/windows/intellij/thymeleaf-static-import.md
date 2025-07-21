---
authors:
  - XIYO
  - XIYO
  - XIYO
dates:
  - '2024-09-10T20:23+0900'
  - '2024-09-08T12:40+0900'
  - '2024-09-07T19:43+0900'
messages:
  - ':art: 리소스 경로를 규격에 맞게 통일'
  - ':art: 로케일 코드 제거하고, 번역된 파일을 기존 처럼 /static/{locale} 구조로 저장'
  - ':globe_with_meridians: 일본어 추가'
title: IntelliJにおけるHTMLの静的リソース認識問題の解決
description: IntelliJでSpring BootプロジェクトのHTMLが静的リソースであるJavaScriptファイルを認識しない問題を解決します。
---
# IntelliJにおけるHTMLの静的リソース認識問題の解決

IntelliJでSpring BootプロジェクトのHTMLが静的リソースであるJavaScriptファイルを認識しない問題を解決します。

コードを記述する際に、IntelliJがJavaScriptファイルを認識しないために不便を感じることがあります。この問題は実際にアプリケーションを実行する際には影響を与えませんが、コーディング中にエラーを引き起こす可能性があるため、解決が必要です。

## 原因

![IntelliJでの静的リソース認識失敗](/static/resources/2024-01-16-13-38-33.png)

Spring BootプロジェクトでHTMLにJavaScriptファイルをインポートする際に、JavaScriptのパスを正しく見つけられない問題が発生します。これはIntelliJのリソースディレクトリ設定が原因です。

## 解決方法

IntelliJの**Project Structure**ウィンドウで`src/main/resources/static`ディレクトリをリソースとして追加します。

![リソースパスを登録する方法](/static/resources/2024-01-16-13-38-45.png)

> **ヒント**
>
> <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Shift</kbd> + <kbd>S</kbd>を押すことで**Project Structure**ウィンドウを開くことができます。

