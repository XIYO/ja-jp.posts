---
title: クラスの静的初期化
description: 私のブログでカテゴリーを作成・管理するコードで使用する静的初期化方法と、より正しいコードに改善した事例を紹介します。
authors:
  - XIYO
  - xiyo
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:57:19+09:00
---
# クラスの静的初期化

私のブログでカテゴリーを作成・管理するコードで使用する静的初期化方法と、より正しいコードに改善した事例を紹介します。

ブログプロジェクトで、カテゴリーを管理するためにクラス構文を活用した[Category.js](https://github.com/XIYO/xiyo.github.io/blob/a1bbc44ebd12986ce1d06d74273c6242efbae4f2/src/lib/post/Category.js "クラス初期化を外部で実行したコード")を設計しました。  
設計時に最も重点を置いた部分は、メンバーの露出最小化でした。
すべてのメンバーに`#`を付けてプライベートとして宣言し、外部から直接アクセスできないようにし、
メンバーの露出が必要な場合は、フィールドはゲッターのみを提供して書き込みを制限し、メソッドは公開メソッドに変換しました。

## 最初の設計

`Category.js`は`new`キーワードを通じたインスタンス化ではなく、[静的メソッドでカテゴリーインスタンスを返す](https://github.com/XIYO/xiyo.github.io/blob/a1bbc44ebd12986ce1d06d74273c6242efbae4f2/src/lib/post/Category.js#L84-L100)構造を望みました。

```js
import Category from '$lib/post/Category.js';

Category.getCategory("Windows") // Windowsカテゴリーインスタンスを返す
```

> 静的メソッドを通じてすでに作成されたカテゴリーインスタンスを取得するデザイン

この方式で使用するには、別途の初期化なしにインポートと同時に[内部で初期化](https://github.com/XIYO/xiyo.github.io/blob/a1bbc44ebd12986ce1d06d74273c6242efbae4f2/src/lib/post/Category.js#L178)が行われる必要がありました。このとき、メソッドを外部に露出せずにインポートと同時に初期化する方法を考えた結果、
- クラス外部に「Symbol」を宣言し、
- クラス内部に「Symbol」をメソッド名として使用した後、
- そのメソッドを実行して外部に露出されない初期化メソッドを実装することができました。

```js data-title="Category.js"
const symbol = Symbol('Category initialization');

export default class Category {
	static [symbol]() {
	    // ...init
	}
}

Category[symbol]();
```

> シンボルを活用したメソッド名定義で外部アクセスを防止した初期化方式

しかし、この方式には欠点がありました。
リフレクションを使用すると初期化メソッドにアクセスでき、
これを通じて初期化が再実行される可能性がありました。
将来、この問題を防ぐための改善が必要でした。

## 静的初期化ブロックによる改善

Javaでは`{}`ブロックを通じて静的メンバーとインスタンスメンバーを初期化できます。
[JavaScriptでもクラス構文に適用](https://github.com/XIYO/xiyo.github.io/blob/ebd7d90f357ef507654a1a6b08aa4ece8f42d0d1/src/lib/post/Category.js#L16-L29 "静的初期化ブロックを使用したコード")してコードをより簡潔にすることができます。

> [!NOTE]
> プロトタイプは即時実行関数式、「IIFE」を使用して静的初期化ロジックを実装できます。

```js data-title="Category.js"
const symbol = Symbol('Category initialization'); // [!code --]

export default class Category {
	static [symbol]() { // [!code --]
	static { // [!code ++]
	    this.#member = data; // 静的初期化でthisキーワード使用可能 // [!code ++]
	    // ...init
	}
}

Category[symbol](); // [!code --]
```

> 静的初期化ブロックを通じたクラス内部での初期化

### JavaとJavaScriptの初期化ブロックの違い

Javaでは2つの初期化ブロックを使用できます：
- `static {}`、静的初期化ブロック
- `{}`、オブジェクト初期化ブロック

一方、JavaScriptでは1つの初期化ブロックのみ使用できます：
- `static {}`、静的初期化ブロック

さらに、JavaとJavaScriptは初期化ブロックでの`this`キーワード使用に違いがあります。
Javaはインスタンス生成後にのみ`this`を使用できますが、
JavaScriptは第一級オブジェクトとして静的初期化ブロックでも`this`を使用して静的メンバーにアクセスできます。
この違いは、JavaScriptが関数型プログラミングの特性をよりよくサポートするためです。
