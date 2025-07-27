---
title: イテレータ
description: コレクションの走査方法を定義する
authors:
  - XIYO
  - xiyo
lastModified: 2025-07-27T21:08:42+09:00
published: 2025-07-22T01:57:19+09:00
---
# イテレータ

コレクションの走査方法を定義する

> [!TIP]
> コレクションとは、配列、リスト、スタック、キューなど複数の要素の集合を意味します。

## いつ使うか？

コード作成時にコレクションを作成する場合、集合を走査する方法を標準的な方法で提供したい時に使用します。

## 比較

### イテレータパターンなしで直接走査を作った場合

```javascript
class KingArr {
	#arr;

	constructor([]) {
		this.#arr = [];
	}

	i = 0;

	// ネーミング規約がないため、独自のネーミングを使用
	get kingElement() {
		if (this.i >= this.#arr.length) {
			return undefined;
		}
		return this.#arr[i++];
	}

	kigeReset() {
		this.i = 0;
	}
}

const myArr = new KingArr();

// MyArrクラスのelementの名前が変更されると、以下のコードも修正が必要
try {
	while (myArr.kingElement)
        console.log(myArr.kingElement);
} catch (e) {
    console.error(e);
} finally {
    myArr.kigeRestart();
}
```

ある開発者が`KingArr`の最初のバージョンを作成しましたが、走査中にエラーが発生する可能性があるため、使用時には常に`try catch`文を使用しなければならない不便さがあります。

`KingArr`の走査方法を知らない開発者は、例外処理なしで走査することもあります。
名前も意味が分かりにくいため、メソッド名が変更される可能性が高く、その場合、これを使用するコードも一緒に修正する必要があります。

### イテレータパターンを適用した場合

すべての言語で実装されており、多くのライブラリもイテレータを使用しているため、イテレータを実装すると互換性があります。

```javascript
class KingArr {
  #arr;
  
  constructor(arr = []) {
    this.#arr = arr;
  }

  // イテレータメソッドを定義
  [Symbol.iterator]() {
    let index = 0;
    const items = this.#arr;

	// nextメソッドを持つオブジェクトを返す
    return {
      // done、valueフィールドを持つオブジェクトを返す
      next() {
        if (index < items.length) {
          return { value: items[index++], done: false };
        }
        return { done: true };
      }
    };
  }
}

// 使用例
const myArr = new KingArr([10, 20, 30, 40]);

// for...ofで安全な走査
for (const item of myArr) {
  console.log(item);  // 10, 20, 30, 40
}

// スプレッド演算子の使用が可能
const arrCopy = [...myArr];
console.log(arrCopy);  // [10, 20, 30, 40]
```

JavaScriptのイテレータ実装は、`Symbol.iterator`をメソッド名として作成するとイテレータになります。

この関数は`next()`という名前の関数を持つオブジェクトを返す必要があり、
`next()`メソッドは返す際に、オブジェクトに2つのフィールド`done`、`value`を含めて返す必要があります。
