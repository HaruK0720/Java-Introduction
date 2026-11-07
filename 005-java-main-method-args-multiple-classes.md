# 【Java入門】mainメソッドの仕組みを解説｜argsの使い方と起動するクラスの指定方法

<br>

## はじめに

Javaのプログラムでよく見かける`public static void main(String[] args)`。実行開始地点として使われることは知っていても、それぞれの単語や`args`の意味はわかりにくいかもしれません。

この記事ではJava 17を前提に、`main`メソッドの宣言、通常のメソッドとの違い、複数クラスの起動方法、コマンドライン引数の受け取り方を解説します。

<br><br><br>

## mainメソッドの宣言を分解する

Java 17で一般的なコマンドラインアプリケーションを起動する際は、起動対象のクラスに次の形式のメソッドを用意します。

```java
public static void main(String[] args) {
    // ここに処理を書く
}
```

それぞれの意味は次のとおりです。

| 要素 | 意味 |
| --- | --- |
| `public` | クラスの外部からアクセスできる |
| `static` | オブジェクトを作らなくても呼び出せる |
| `void` | 呼び出し元に値を返さない |
| `main` | 起動時に呼び出されるメソッド名 |
| `String[]` | 文字列を複数格納できる配列型 |
| `args` | 受け取った配列を参照する引数名 |

`String[] args`は、「文字列の配列を`args`という名前で受け取る」という意味です。`args`自体は予約語ではないため、`String[] values`のように別の名前にもできます。

ただし、**Java 17の通常の起動方法では、`main`の名前と`public`・`static`・`void`、文字列配列を受け取る形式が重要**です。

<br><br>

## mainメソッドと通常のメソッドの違い

`main`もJavaのメソッドの一つですが、プログラムの**実行開始地点（エントリーポイント）**として特別な役割を持っています。

| 比較 | `main`メソッド | 通常のメソッド |
| --- | --- | --- |
| 呼び出され方 | `java`コマンドによる起動時に呼ばれる | ほかの処理から呼び出す |
| 名前 | 起動用には`main`とする | 用途に応じて決められる |
| 引数 | 起動用には`String`配列を受け取る | 必要に応じて決められる |
| 戻り値 | 起動用には`void` | `void`以外も指定できる |

例えば、次のようなメソッドは`main`とは別の通常のメソッドです。

```java
public static void printMessage(String name, String subject) {
    System.out.println(name + "さんの学習科目: " + subject);
}
```

このメソッドは、受け取った名前と科目を表示します。`static`が付いていても、それだけで実行開始地点になるわけではありません。

<br><br><br>

## String[] argsでコマンドライン引数を受け取る

**コマンドライン引数**は、プログラムを起動するときに指定する値です。Javaでは、クラス名の後ろに書いた値が`args`に入ります。

### サンプルコード

**ファイル名：`MessageApp.java`**

```java
public class MessageApp {
    public static void main(String[] args) {
        System.out.println("受け取った引数: " + args.length + "個");

        if (args.length < 2) {
            System.out.println("使い方: java MessageApp 名前 科目");
            return;
        }

        printMessage(args[0], args[1]);
    }

    public static void printMessage(String name, String subject) {
        System.out.println(name + "さんの学習科目: " + subject);
    }
}
```

保存したフォルダでコンパイルし、引数を指定して実行します。

```bash
javac -encoding UTF-8 MessageApp.java
java MessageApp Taro Java
```

**実行結果**

```text
受け取った引数: 2個
Taroさんの学習科目: Java
```

<br>

### 引数が渡される仕組み

`java MessageApp Taro Java`の場合、`MessageApp`は起動するクラス名であり、`args`には入りません。

- `args.length`：引数の個数（この例では`2`）
- `args[0]`：最初の引数（`"Taro"`）
- `args[1]`：2番目の引数（`"Java"`）

配列の位置は**0から数える**ことに注意しましょう。受け取った文字列は、`printMessage(args[0], args[1]);`によって通常のメソッドに渡されます。

コード中の`if`は「引数が2個未満なら」という条件分岐で、`return;`はそこで`main`の処理を終了する命令です。

<br>

### 引数を渡さなかった場合

```bash
java MessageApp
```

```text
受け取った引数: 0個
使い方: java MessageApp 名前 科目
```

引数がないとき、起動時の`args`は要素数0の配列です。`args[0]`などをそのまま参照すると実行時エラーになるため、`args.length`で個数を確認しています。

なお、`java MessageApp "Taro Yamada" Java`のように引用符で囲むと、空白を含む名前を1つの引数として渡せます。引数が`100`のように見えても、`args`で受け取る時点では文字列です。

<br><br>

## 複数のクラスがあるときは、起動するクラスを選ぶ

Javaでは、複数のクラスを作成できます。また、**複数のクラスがそれぞれ`main`メソッドを持つことも可能**です。

先ほどの`MessageApp.java`に加えて、次のファイルを用意します。

**ファイル名：`HelpApp.java`**

```java
public class HelpApp {
    public static void main(String[] args) {
        System.out.println("使い方: java MessageApp 名前 科目");
    }
}
```

同じフォルダに2つのファイルを保存したら、次のようにコンパイルできます。

```bash
javac -encoding UTF-8 MessageApp.java HelpApp.java
```

起動したいクラス名を`java`コマンドで指定します。

```bash
java HelpApp
```

**実行結果**

```text
使い方: java MessageApp 名前 科目
```

一方、`java MessageApp Taro Java`なら`MessageApp`の`main`が実行されます。**すべてのクラスの`main`が順番に実行されるわけではありません。**

補助的な役割のクラスには`main`がなくても構いません。その場合は、通常、そのクラスを直接起動するのではなく、起動されたクラスから機能を利用します。

<br><br>

## よくある間違い

### ① 引数の範囲外を参照する

引数を1個しか渡していないときに`args[1]`を参照すると、`ArrayIndexOutOfBoundsException`が発生します。使う前に`args.length`を確認しましょう。

### ② argsを必ず決まった名前だと思う

`args`は慣習的な名前であり、名前そのものは変更可能です。ただし、メソッド内で参照する名前も合わせる必要があります。

### ③ クラス名に.javaや.classを付ける

コンパイル済みクラスを実行する場合、基本的には`java MessageApp`のようにクラス名を指定します。`java MessageApp.java`は、Java 11以降の**ソースファイル直接実行**という別の起動方法です。

<br><br><br>

## 練習問題

### 問題

`ReverseArgs.java`を作成し、コマンドライン引数として受け取った**2つの単語を逆の順番で表示**してください。引数が2個未満なら、案内メッセージを表示して終了させます。

実行コマンド：

```bash
java ReverseArgs red blue
```

**期待する実行結果**

```text
2番目: blue
1番目: red
```

ヒント：`args[0]`が最初の単語、`args[1]`が次の単語です。

<br>

### 解答例

```java
public class ReverseArgs {
    public static void main(String[] args) {
        if (args.length < 2) {
            System.out.println("2つの単語を指定してください");
            return;
        }

        System.out.println("2番目: " + args[1]);
        System.out.println("1番目: " + args[0]);
    }
}
```

`args[1]`を先に、`args[0]`を後に表示することで、入力順とは逆の並びになります。引数の個数を先に確認することで、引数不足によるエラーも防いでいます。

<br><br>

## まとめ

- `main`は、Java 17の基本的なアプリケーションの実行開始地点となるメソッドです。
- `public static void main(String[] args)`の各部分には、アクセス範囲・呼び出し方・戻り値・引数の指定という役割があります。
- `args`は起動時に渡された文字列の配列で、`args[0]`から順番に取り出せます。
- 複数のクラスがあっても、`java クラス名`で起動対象を選びます。
- 引数を参照する前に、`args.length`で個数を確認すると安全です。

<br><br>

## 参考資料

- [Oracle Java SE 17 - javaコマンド](https://docs.oracle.com/javase/jp/17/docs/specs/man/java.html)
- [Java言語仕様 Java SE 17 - Chapter 12. Execution](https://docs.oracle.com/javase/specs/jls/se17/html/jls-12.html)
- [Dev.java - Defining Methods](https://dev.java/learn/language/oop/classes-objects/defining-methods/)

