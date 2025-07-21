---
title: クッキー送信シナリオ分析
description: 'すべてのクッキーは次の共通オプションを持ちます：'
authors:
  - XIYO
  - XIYO
  - XIYO
  - XIYO
dates:
  - '2025-06-15T13:04:31.601Z'
  - '2025-06-15T13:01:45.902Z'
  - 2025-06-15T10:48+0900
  - 2025-06-07T14:58+0900
tags: []
messages:
  - '✨ クッキー送信シナリオ分析文書の内容追加：SameSite設定とドメイン属性によるクッキー送信可否の整理'
  - ✨ クッキー送信シナリオ分析文書追加
  - \U0001F921
  - 📝 草案
---
# クッキー送信シナリオ分析

この文書は、クッキー送信シナリオを分析し、さまざまなSameSite設定とドメイン属性に応じたクッキー送信の可否を整理します。この分析は`https://api.hello.dev`と`https://hello.dev`間のリクエストを基準としています。

## 前提条件

すべてのクッキーは次の共通オプションを持ちます：
- **Secure=true**: HTTPS接続でのみクッキー送信

ブラウザは**同一サイト**（originとtargetが同じ登録ドメインhello.devを共有）間のリクエストでのみすべてのSameSite設定クッキーを送信するため、ここではSameSiteによるブロックはありません。クッキーのDomain属性を指定すると、そのドメインとすべてのサブドメインにクッキーが送信されます。以下の表で✅はクッキー送信、🚫は送信されないことを示します。

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

¹ 認証情報を含む（Fetch APIはcredentials: includeオプションが必要）

**注意：** ドメイン属性を指定すると、指定されたドメインとすべてのサブドメインにクッキーが送信されます。