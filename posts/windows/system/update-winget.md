---
authors:
  - XIYO
  - XIYO
  - XIYO
dates:
  - '2024-09-18T11:16+0900'
  - '2024-09-08T12:40+0900'
  - '2024-09-07T19:43+0900'
messages:
  - ':truck: 이미지 경로를 전부 /static/resource 로 이동'
  - ':art: 로케일 코드 제거하고, 번역된 파일을 기존 처럼 /static/{locale} 구조로 저장'
  - ':globe_with_meridians: 일본어 추가'
title: WinGet 実行エラーの解決方法
description: コンピュータが遅くなったので、久しぶりに Windows を再インストールしました。
---
# WinGet 実行エラーの解決方法

コンピュータが遅くなったので、久しぶりに Windows を再インストールしました。  
そして `winget` コマンドでパッケージをインストールしようとしたところ、実行すらできない問題が発生しました。

`winget -v` コマンドは正常に動作しますが、`winget install` コマンドは実行できません。

## 解決方法

アプリインストーラーを更新する必要があります。

![アプリストアで全アプリの更新をダウンロード中](/static/resources/update-winget-20240918110056451.png)

0. Microsoft Store を起動します。  
1. ライブラリで「更新のダウンロード」をクリックします。

