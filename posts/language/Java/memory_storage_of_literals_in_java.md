---
authors:
  - XIYO
dates:
  - '2024-10-05T22:08+0900'
messages:
  - ':memo: new post'
title: リテラルのメモリ格納方式
description: >-
  リテラルはプログラミング言語で変数に直接割り当てられる固定値を意味します。この記事ではJavaのリテラルがメモリにどのように格納され管理されるかを見ていきます。
---
# リテラルのメモリ格納方式

リテラルはプログラミング言語で変数に直接割り当てられる固定値を意味します。この記事ではJavaのリテラルがメモリにどのように格納され管理されるかを見ていきます。

## リテラルとは？

リテラルはコードで値として直接現れるデータを指します。例えば、数字`10`、文字列`"Hello"`、論理値`true`などはすべてリテラルです。簡単に言えば、リテラルはコードで使用されるデータそのものです。

リテラルの代表的な種類は次のとおりです：

- **整数リテラル**: `10`、`-42`、`0`、`9999L`
- **実数リテラル**: `3.14f`、`0.5`
- **文字リテラル**: `'A'`、`'B'`
- **文字列リテラル**: `"Hello"`、`"World"`
- **ブーリアンリテラル**: `true`、`false`

## リテラルの格納方式

リテラルがメモリに格納される方式は、変数が基本型かラッパークラスまたは文字列かによって異なります。

### 基本型変数

基本型変数にリテラルを代入すると、その値は変数のメモリ空間に直接格納されます。例えば、整数リテラル`10`を基本型変数に割り当てると、変数のメモリ空間に`10`という値が直接格納されます。これは処理速度が速く効率的です。

**コード例:**
```java
public class Main {
    public static void main() {
        int intVal = 3;
    }
}
```

**メモリダイアグラム:**

[![](https://mermaid.ink/img/pako:eNpVULFOwzAQ_RXrJpCiKHHqNvEIrJ2KGCAMJnabiMSuXEdQomydkNhZ-g8dGOCb2v5DL4lU1JNlv3d67-l8DWRGKuAwL81blgvryP1NqgnWqn5ZWLHMya0oy5kT2etTCh0mPUnhedB1JQurMlcYfXZfJExFodHcPX6F19X1hburQrsHUaJoAJxEh-032f9tjp-_ZP-1O2x_jpvdhU1pORAE4EGlLGZL_EvTtVNwuapUChyhFBYHTnWLOlE7M1vrDLiztfLAmnqRA5-LcoWsXkrh1F0hcPLq3F0K_WjMP1eycMZOh9X1G-w1wBt4B54EfsLoKKaTgMZROGYerIHTkPrJmOIJJ0E8DuKo9eCjT438MGDBiLIwYiyJ6Ii1J9YYgVQ?type=png)](https://mermaid.live/edit#pako:eNpVULFOwzAQ_RXrJpCiKHHqNvEIrJ2KGCAMJnabiMSuXEdQomydkNhZ-g8dGOCb2v5DL4lU1JNlv3d67-l8DWRGKuAwL81blgvryP1NqgnWqn5ZWLHMya0oy5kT2etTCh0mPUnhedB1JQurMlcYfXZfJExFodHcPX6F19X1hburQrsHUaJoAJxEh-032f9tjp-_ZP-1O2x_jpvdhU1pORAE4EGlLGZL_EvTtVNwuapUChyhFBYHTnWLOlE7M1vrDLiztfLAmnqRA5-LcoWsXkrh1F0hcPLq3F0K_WjMP1eycMZOh9X1G-w1wBt4B54EfsLoKKaTgMZROGYerIHTkPrJmOIJJ0E8DuKo9eCjT438MGDBiLIwYiyJ6Ii1J9YYgVQ)

> 基本型変数はコールスタックにビットデータを直接格納します。

### ラッパークラスと文字列

基本型の参照型であるラッパークラス（Integer、Doubleなど）と文字列クラスは、定数プール（Constant Pool）という特別な空間に格納されます。定数プールに同じ値がすでに存在する場合、既存のアドレスを返してメモリを節約します。

**コード例:**
```java
public class Main {
    public static void main(String[] args) {
        Integer intVal = 3;
        String str = "hello";
    }
}
```

**メモリダイアグラム:**

[![](https://mermaid.ink/img/pako:eNqFUj1PwzAQ_SvWLQWprfLRtEkGBmBhqIRUxABhMInbRLh25TiCUnWrGBDsLJ34Ax0YQOIftf0POE6b0gLiFMX3rHf37sk3gpBHBHzoUn4bxlhIdHYYMKQiza57Ag9idIQp7Ugc3lwGkOdIgwCuCl4eUSJIKBPOyuqtDm2cMFWcH_W--u3tb1XnkTB5jqkinTBJekSsLny0eP1cPDz94KdSKHJHioT1cvArkbCoAGWya42zVGImTznPtdcQ5XirE00kEZgWI65HsxfTFzT_mCwf39H8ebaYvi0ns7JMa-7oFfPuqK5M_C2eakKhra1WYkIpr_wvv7FczIxqtYNvXlbTSaHvSxmoQp8I9VCRWoxRTgpAxqRPAvBVGmGhXj9gY8XDmeSdIQvBlyIjVRA868XgdzFNFcoGEZbkOMHKfb-8HWB2wfkGkyiRXLSLPdTrqDngj-AOfM-oe47VcK2WYbm22XSqMATfMq2617TUZ7YMt2m49rgK97qrXTcNx2hYjmk7jmdbDWf8BU0T910?type=png)](https://mermaid.live/edit#pako:eNqFUj1PwzAQ_SvWLQWprfLRtEkGBmBhqIRUxABhMInbRLh25TiCUnWrGBDsLJ34Ax0YQOIftf0POE6b0gLiFMX3rHf37sk3gpBHBHzoUn4bxlhIdHYYMKQiza57Ag9idIQp7Ugc3lwGkOdIgwCuCl4eUSJIKBPOyuqtDm2cMFWcH_W--u3tb1XnkTB5jqkinTBJekSsLny0eP1cPDz94KdSKHJHioT1cvArkbCoAGWya42zVGImTznPtdcQ5XirE00kEZgWI65HsxfTFzT_mCwf39H8ebaYvi0ns7JMa-7oFfPuqK5M_C2eakKhra1WYkIpr_wvv7FczIxqtYNvXlbTSaHvSxmoQp8I9VCRWoxRTgpAxqRPAvBVGmGhXj9gY8XDmeSdIQvBlyIjVRA868XgdzFNFcoGEZbkOMHKfb-8HWB2wfkGkyiRXLSLPdTrqDngj-AOfM-oe47VcK2WYbm22XSqMATfMq2617TUZ7YMt2m49rgK97qrXTcNx2hYjmk7jmdbDWf8BU0T910)

> ラッパークラスと文字列は定数プールに格納された値を参照します。

## ラッパークラスと文字列の比較

ラッパークラスと文字列リテラルは定数プールのアドレスを参照するため、同じ値を複数回生成しても常に同じインスタンスを参照します。一方、`new`キーワードを使用してオブジェクトを生成すると、定数プールの代わりにヒープメモリに新しいオブジェクトが生成されます。

**コード例:**
```java
public class ConstantPoolTest {  
    public static void main(String[] args) {  
        A a = new A();  
        B b = new B();  
  
        System.out.println(a.instanceStr == b.instanceStr);  // true  
        System.out.println(a.instanceStr == b.newStr);       // false  
        System.out.println(a.instanceStr == b.internStr);    // true  
        System.out.println(a.instanceStr.equals(b.newStr));  // true  

        System.out.println(a.instanceInt == b.instanceInt);  // true  
        System.out.println(a.instanceInt == b.newInt);       // false  
        System.out.println(a.instanceInt == b.internInt);    // true  
        System.out.println(a.instanceInt.equals(b.newInt));  // true  
    }  
}  
  
class A {  
    String instanceStr = "instanceStr";  
    Integer instanceInt = 1;  
}  
  
class B {  
    String instanceStr = "instanceStr";  
    String newStr = new String("instanceStr");  
    String internStr = newStr.intern();  

    Integer instanceInt = 1;  
    Integer newInt = new Integer(1);  
    Integer internInt = newInt.intValue();  
}
```
> `intern()`メソッドを使用すると、文字列定数プールで同じ値を見つけてアドレスを返します。

リテラルで生成されたオブジェクトは同じ定数プールアドレスを共有するため比較結果が「真」になりますが、`new`キーワードを使用して生成したオブジェクトはヒープメモリに別々に生成されるため比較結果が「偽」になります。