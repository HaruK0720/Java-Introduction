# 【Java入門】変数の宣言・初期化・代入・再代入の基本

<br>

## はじめに

Javaでは、年齢や点数、在庫数など、プログラムの中で使う値を**変数**に保存できます。値をそのまま何度も書くのではなく、名前を付けて管理できるのが便利なところです。

この記事ではJava 17を前提に、`int age = 19;`を例として、変数の**宣言・初期化・代入・再代入**を順番に解説します。

<br><br><br>

## 変数とは？

変数は、値を保存しておくための、名前の付いた場所です。例えば、`age`という変数に年齢を入れておけば、その名前を使って年齢を表示したり、後から値を変更したりできます。

Javaの変数には**型（データ型）**があり、どのような種類の値を扱うかが決まっています。

| 型 | 扱う値の例 | 書き方 |
| --- | --- | --- |
| `int` | 整数 | `int age = 19;` |
| `double` | 小数 | `double height = 170.5;` |
| `String` | 文字列 | `String name = "Taro";` |
| `boolean` | 真偽値 | `boolean completed = false;` |

今回は、メソッドの中で使う**ローカル変数**を扱います。

<br><br>

## 宣言・初期化・代入はどう違う？

### ① 宣言：変数を使う準備

```java
int age;
```

`int`が型、`age`が変数名です。このように型と名前を指定して変数を用意することを**宣言**といいます。

ただし、メソッド内のローカル変数は、宣言しただけでは値を使えません。読み出す前に値を代入する必要があります。

<br>

### ② 代入：変数に値を入れる

```java
age = 19;
```

`=`は、右側の値を左側の変数に入れる**代入演算子**です。数学の「左右が等しい」という意味ではありません。

<br>

### ③ 初期化：最初の値を設定する

宣言と同時に最初の値を入れることもできます。

```java
int age = 19;
```

この場合、`age`の**初期値**は`19`です。ここまでを1行で書くのが一般的ですが、後から値を設定する必要がある場合は、宣言と代入を分けることもできます。

<br><br>

## 再代入すると値はどう変わる？

すでに値が入っている変数へ、別の値を入れることを**再代入**と呼びます。

```java
int age = 19;
age = 20;
```

2行目では型の`int`を書きません。すでに宣言済みの`age`へ新しい値を入れているためです。これ以降、`age`の値は`20`になります。

<br><br>

## サンプルコードで確認する

**ファイル名：`VariableBasics.java`**

```java
public class VariableBasics {
    public static void main(String[] args) {
        int age = 19;
        System.out.println("最初の年齢: " + age);

        age = 20;
        System.out.println("変更後の年齢: " + age);

        int studyMinutes;
        studyMinutes = 30;
        System.out.println("学習時間: " + studyMinutes + "分");

        studyMinutes = 45;
        System.out.println("更新後: " + studyMinutes + "分");
    }
}
```

**実行結果**

```text
最初の年齢: 19
変更後の年齢: 20
学習時間: 30分
更新後: 45分
```

<br>

### 値の変化を追ってみよう

| 処理 | 変数 | その時点の値 |
| --- | --- | --- |
| `int age = 19;` | `age` | `19` |
| `age = 20;` | `age` | `20` |
| `int studyMinutes;` | `studyMinutes` | まだ代入されていない |
| `studyMinutes = 30;` | `studyMinutes` | `30` |
| `studyMinutes = 45;` | `studyMinutes` | `45` |

`System.out.println()`は、その行が実行された時点の値を表示します。後から再代入しても、すでに表示された内容が書き換わるわけではありません。

<br><br><br>

## 初心者が間違えやすいポイント

### ① 代入前にローカル変数を使う

```java
int age;
System.out.println(age); // コンパイルエラー
```

メソッド内のローカル変数は、**値が代入されたと確認できる状態**でなければ読み出せません。`age = 19;`などで値を入れてから使いましょう。

<br>

### ② 再代入のときにもう一度宣言する

```java
int age = 19;
int age = 20; // 同じ範囲では再宣言できない
```

同じスコープ（変数を使用できる範囲）に同じ名前のローカル変数を再宣言すると、コンパイルエラーになります。値を変更するなら`age = 20;`です。

<br>

### ③ 型と合わない値を入れる

```java
int age = 19;
// age = "20"; // String型なので代入できない
```

`int`の変数には文字列の`"20"`をそのまま代入できません。**値は変更できても、宣言した変数の型が変わるわけではない**ためです。

また、`final int age = 19;`のように`final`を付けた変数には、初期化後の再代入ができません。

<br><br><br>

## 練習問題

### 問題

所持金を表す`balance`という`int`型の変数を作り、初期値を`1000`にしてください。

その後、300円使い、さらに200円入金したときの残高を、**再代入を使って**順番に表示してください。

**期待する実行結果**

```text
最初の残高: 1000円
購入後: 700円
入金後: 900円
```

ヒント：`balance = balance - 300;`は、現在の`balance`から300を引いた結果を、同じ変数へ代入するという意味です。

<br>

### 解答例

**ファイル名：`BalancePractice.java`**

```java
public class BalancePractice {
    public static void main(String[] args) {
        int balance = 1000;
        System.out.println("最初の残高: " + balance + "円");

        balance = balance - 300;
        System.out.println("購入後: " + balance + "円");

        balance = balance + 200;
        System.out.println("入金後: " + balance + "円");
    }
}
```

`balance = balance - 300;`では、右側の古い値`1000`を使って計算し、その結果の`700`を左側へ代入します。次の行では更新後の`700`を使うため、`700 + 200`で`900`になります。

<br><br>

## まとめ

- **宣言**は、型と名前を決めて変数を用意することです。
- **初期化**は最初の値を設定すること、**代入**は変数に値を入れることです。
- **再代入**では、型を書き直さずに新しい値を設定します。
- ローカル変数は、値が代入される前に読み出せません。
- 再代入しても変数の型は変わらず、`final`を付けた変数には再代入できません。

<br><br>

## 参考資料

- [Dev.java - Creating Variables and Naming Them](https://dev.java/learn/language/constructs/basics/variables/)
- [Java SE 17 言語仕様 - 14.4 Local Variable Declarations](https://docs.oracle.com/javase/specs/jls/se17/html/jls-14.html#jls-14.4)
- [Java SE 17 言語仕様 - 15.26 Assignment Operators](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.26)

