---
title: クッキー送信シナリオ分析
description: >-
  このドキュメントはクッキー送信シナリオを分析し、さまざまなSameSite設定とドメイン属性によるクッキー送信可否を整理します。この分析は`https://api.hello.dev`と`https://hello.dev`間のリクエストを基準としています。
authors:
  - XIYO
  - xiyo
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:33:12+09:00
---
# クッキー送信シナリオ分析

このドキュメントはクッキー送信シナリオを分析し、さまざまなSameSite設定とドメイン属性によるクッキー送信可否を整理します。この分析は`https://api.hello.dev`と`https://hello.dev`間のリクエストを基準としています。

## 前提条件

すべてのクッキーは次の共通オプションを持ちます：
- **Secure=true**：HTTPS接続でのみクッキーを送信

ブラウザは**同一サイト**（originとtargetが同じ登録ドメインhello.devを共有）間のリクエストでのみすべてのSameSite設定クッキーを送信するため、ここではSameSiteによるブロックはありません。クッキーのDomain属性を指定すると、該当ドメインとすべてのサブドメインにクッキーが送信されます。以下の表で✅はクッキー送信、🚫は送信されないことを示します。

## `https://api.hello.dev` → `https://api.hello.dev`

|**Domain**|**SameSite**|**Form GET**|**Form POST**|**Fetch GET**|**Fetch POST**|
|---|---|---|---|---|---|
|api.hello.dev|Strict|✅|✅|✅¹|✅¹|
|api.hello.dev|Lax|✅|✅|✅¹|✅¹|
|api.hello.dev|None|✅|✅|✅¹|✅¹|
|.hello.dev|Strict|✅|✅|✅¹|✅¹|
|.hello.dev|Lax|✅|✅|✅¹|✅¹|
|.hello.dev|None|✅|✅|✅¹|✅¹|

## `https://api.hello.dev` → `https://*.hello.dev`

|**Domain**|**SameSite**|**Form GET**|**Form POST**|**Fetch GET**|**Fetch POST**|
|---|---|---|---|---|---|
|api.hello.dev|Strict|🚫|🚫|🚫|🚫|
|api.hello.dev|Lax|🚫|🚫|🚫|🚫|
|api.hello.dev|None|🚫|🚫|🚫|🚫|
|.hello.dev|Strict|✅|✅|✅¹|✅¹|
|.hello.dev|Lax|✅|✅|✅¹|✅¹|
|.hello.dev|None|✅|✅|✅¹|✅¹|

## `https://api.hello.dev` → `https://hello.dev`

|**Domain**|**SameSite**|**Form GET**|**Form POST**|**Fetch GET**|**Fetch POST**|
|---|---|---|---|---|---|
|api.hello.dev|Strict|🚫|🚫|🚫|🚫|
|api.hello.dev|Lax|🚫|🚫|🚫|🚫|
|api.hello.dev|None|🚫|🚫|🚫|🚫|
|.hello.dev|Strict|✅|✅|✅¹|✅¹|
|.hello.dev|Lax|✅|✅|✅¹|✅¹|
|.hello.dev|None|✅|✅|✅¹|✅¹|

## `https://hello.dev` → `https://api.hello.dev`

|**Domain**|**SameSite**|**Form GET**|**Form POST**|**Fetch GET**|**Fetch POST**|
|---|---|---|---|---|---|
|hello.dev|Strict|🚫|🚫|🚫|🚫|
|hello.dev|Lax|🚫|🚫|🚫|🚫|
|hello.dev|None|🚫|🚫|🚫|🚫|
|.hello.dev|Strict|✅|✅|✅¹|✅¹|
|.hello.dev|Lax|✅|✅|✅¹|✅¹|
|.hello.dev|None|✅|✅|✅¹|✅¹|

## `https://hello.dev` → `https://*.hello.dev`

|**Domain**|**SameSite**|**Form GET**|**Form POST**|**Fetch GET**|**Fetch POST**|
|---|---|---|---|---|---|
|hello.dev|Strict|🚫|🚫|🚫|🚫|
|hello.dev|Lax|🚫|🚫|🚫|🚫|
|hello.dev|None|🚫|🚫|🚫|🚫|
|.hello.dev|Strict|✅|✅|✅¹|✅¹|
|.hello.dev|Lax|✅|✅|✅¹|✅¹|
|.hello.dev|None|✅|✅|✅¹|✅¹|

---

## 脚注

¹ 認証情報付き（Fetch APIはcredentials: includeオプションが必要）

**注意：**ドメイン属性を指定すると、指定ドメインとすべてのサブドメインにクッキーが送信されます。
