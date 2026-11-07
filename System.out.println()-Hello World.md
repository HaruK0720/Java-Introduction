# 【Java入門】System.out.println()でHello Worldを出力する方法 

## はじめに

Javaの学習を始めるとき、最初によく登場するのが「Hello World」という文字列を画面に表示するプログラムです。

Javaでは、`System.out.println()`を使用することで、文字列や数値などを簡単に出力できます。<br>
ただし、Javaでは出力する命令を書くだけでなく、クラスやメソッドと呼ばれる仕組みを使ってプログラムを構成します。


この記事では、以下の内容を解説します。

- Javaプログラムの基本的な構造
- `public class Main`と`main`メソッドの役割
- `System.out.println()`の基本的な使い方
- `print()`と`println()`の違い
- 初心者が間違えやすいポイント

## Javaプログラムの基本構造

Javaでプログラムを書くとき、まず登場するのが次のようなコードです。

```java
public class Main {

}
```

初めて見ると、何をしているのかわかりにくいかもしれません。

これは、**`Main`という名前のクラスを定義しているコード**です。

### クラスとは？

クラスとは、プログラムで扱うデータや処理をまとめるための仕組みです。

Javaでは、基本的にクラスの中にメソッドなどを定義してプログラムを作成します。<br>
メソッドとは、特定の処理をまとめたものです。

今回のような簡単なプログラムでは、まず「クラスはプログラムを構成するための基本的なまとまり」と理解しておけば十分です。

### public class Mainの意味

それぞれの要素には、次のような役割があります。

| 要素 | 意味 |
| --- | --- |
| `public` | ほかのクラスからも利用できるようにするアクセス修飾子 |
| `class` | クラスを定義するためのキーワード |
| `Main` | 定義するクラスの名前 |
| `{ }` | クラスの中身を記述する範囲 |

`Main`という名前は特別な決まりではなく、別の名前にすることもできます。

ただし、**`public`を付けたトップレベルのクラスは、クラス名とJavaファイル名を一致させる必要があります。**

今回の場合、ファイル名は`Main.java`になります。

### 波括弧 { } の役割

Javaでは、`{`と`}`を使って処理や定義の範囲を表します。

```java
public class Main {
    // この中にメソッドなどを定義する
}
```

`{`が範囲の始まり、`}`が範囲の終わりです。

なお、最初に示した空のクラスも文法上は正しいコードなので、コンパイルできます。<br>
しかし、まだ実行する処理が書かれていないため、今回の方法ではプログラムを開始できません。

そこで必要になるのが、次に説明する`main`メソッドです。

## mainメソッドとは？

Javaの基本的なプログラムでは、処理の開始地点として`main`メソッドを使用します。

```java
public class Main {
    public static void main(String[] args) {

    }
}
```

それぞれの要素の意味を確認しましょう。

| 要素 | 意味 |
| --- | --- |
| `public` | ほかのクラスからアクセスできることを示す |
| `static` | オブジェクトを作成せずに呼び出せることを示す |
| `void` | 戻り値がないことを示す |
| `main` | プログラムの実行開始地点となるメソッド名 |
| `String[] args` | コマンドラインから渡された文字列を受け取るための引数 |

「戻り値」とは、メソッドが処理結果として呼び出し元に返す値のことです。

また、オブジェクトとは、クラスをもとに作られる実体のことです。<br>
これらの詳しい仕組みは、今後のメソッドやオブジェクト指向の学習で扱います。

今は、**`main`メソッドの中に書いた処理が、プログラムを実行したときに呼び出される**という点を押さえておきましょう。

## System.out.println()とは？

`System.out.println()`は、文字列や数値などを**標準出力に表示するためのメソッド**です。

標準出力とは、プログラムが実行結果などを書き出すための出力先のことです。<br>
通常は、ターミナルや開発環境のコンソールなどに表示されます。

基本的な書き方は次のとおりです。

```java
System.out.println("Hello World");
```

この文を`main`メソッドの中に記述して実行すると、次のように表示されます。

```text
Hello World
```

`println()`には、**出力した内容の最後に自動的に改行を追加する**という特徴があります。

### 構文の意味

`System.out.println()`も、いくつかの要素で構成されています。

| 要素 | 役割 |
| --- | --- |
| `System` | Javaに標準で用意されているクラス |
| `out` | 標準出力を扱うためのフィールド |
| `println()` | 内容を出力して改行するメソッド |
| `""` | 文字列を囲むダブルクォーテーション |
| `;` | 文の終わりを示すセミコロン |

フィールドとは、クラスが持つデータなどを表す変数のことです。

今の段階では、`System.out.println()`を使うことで文字や数値を出力できると理解しておけば十分です。

### 文字列と数値の違い

文字列を出力するときは、ダブルクォーテーション（`"`）で囲みます。

```java
System.out.println("Java");
```

一方、数値はダブルクォーテーションで囲まずに出力することもできます。

```java
System.out.println(100);
```

`"100"`は文字列、`100`は整数として扱われます。<br>
見た目が似ていても、プログラム内部での扱いは異なります。

## Hello Worldを出力してみよう

ここまで学んだクラス、`main`メソッド、`System.out.println()`を組み合わせて、実際にプログラムを作成してみましょう。

### サンプルコード

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

### 出力結果

```text
Hello World
```

### コードの動作

プログラムの構造を整理すると、次のようになります。

1. `public class Main`でクラスを定義する。
2. クラスの中に`main`メソッドを定義する。
3. `main`メソッドの中に出力する処理を記述する。
4. プログラムを実行すると、`main`メソッドが呼び出される。
5. `System.out.println()`によって文字列が出力される。

ここで重要なのは、**クラスとメソッドの波括弧がそれぞれ対応していること**です。

外側の`{ }`はクラスの範囲を、内側の`{ }`は`main`メソッドの範囲を表します。

### Javaプログラムを実行する方法

Java 17のJDKがインストールされている場合、コードを`Main.java`というファイル名で保存します。

ターミナルでファイルを保存した場所に移動し、次のコマンドを実行します。

```text
javac Main.java
java Main
```

`javac Main.java`は、Javaのソースコードをコンパイルするコマンドです。

コンパイルとは、ソースコードをJava仮想マシンが実行できる形式に変換する処理です。<br>
コンパイルに成功すると`Main.class`というファイルが生成され、`java Main`で実行できます。

## print()とprintln()の違い

Javaには、`println()`と似たメソッドとして`print()`も用意されています。

この2つの違いは、**出力後に自動で改行するかどうか**です。

| メソッド | 動作 |
| --- | --- |
| `print()` | 内容を出力し、改行しない |
| `println()` | 内容を出力し、最後に改行する |

実際のコードで比較してみましょう。

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("Hello ");
        System.out.println("World!");
        System.out.println("Java 17");
    }
}
```

### 出力結果

```text
Hello World!
Java 17
```

### なぜこの結果になるのか？

処理の流れを順番に確認します。

1. `print("Hello ")`で`Hello `を出力する。改行はしない。
2. `println("World!")`で、その続きに`World!`を出力して改行する。
3. `println("Java 17")`で、次の行に`Java 17`を出力する。

最初の`print()`では改行されないため、次の`World!`が同じ行に表示されます。

なお、`Hello `の末尾には半角スペースが入っています。<br>
このスペースがなければ、出力結果は`HelloWorld!`になります。

## 初心者が間違えやすいポイント

### ① 文字列をダブルクォーテーションで囲み忘れる

次の書き方は誤りです。

```java
System.out.println(Hello World);
```

文字列として扱うには、ダブルクォーテーションで囲む必要があります。

```java
System.out.println("Hello World");
```

### ② セミコロンを忘れる

Javaでは、通常、文の終わりにセミコロン（`;`）を記述します。

```java
System.out.println("Hello World");
```

セミコロンを書き忘れると、コンパイルエラーになります。

### ③ 大文字と小文字を間違える

Javaでは、大文字と小文字が区別されます。

例えば、`System`を`system`と書いたり、`println`を`Println`と書いたりすると、正しく認識されません。

### ④ 波括弧の対応を間違える

クラスやメソッドの`{ }`が正しく対応していないと、コンパイルエラーになることがあります。

次のようにインデント（字下げ）を使用すると、構造を把握しやすくなります。

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

## 練習問題

今回学んだ`print()`と`println()`を使って、次の出力結果になるプログラムを作成してください。

### 問題

以下の条件を満たすプログラムを作成してください。

- `Good `と`morning!`を別々の文で出力する。
- 2つの文字列を同じ行に表示する。
- 次の行に`Let's learn Java.`と表示する。
- `Main`クラスと`main`メソッドも自分で記述する。

**期待する出力結果**

```text
Good morning!
Let's learn Java.
```

<details>
<summary>ヒントを見る</summary>

最初の文字列を`print()`で出力すると、改行せずに次の文字列を続けて表示できます。

2つ目の文字列を出力したあとに改行するには、`println()`を使用します。

</details>

### 解答例

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("Good ");
        System.out.println("morning!");
        System.out.println("Let's learn Java.");
    }
}
```

### 解説

最初の`print()`は改行しないため、続く`println()`の内容が同じ行に表示されます。

2つ目の`println()`で改行されるので、最後の文字列は次の行に表示されます。<br>
このように、`print()`と`println()`を組み合わせることで、出力する位置を調整できます。

また、今回の練習では`Main`クラスと`main`メソッドも自分で記述することで、Javaプログラムの基本構造を復習できます。

## まとめ

今回は、Javaプログラムの基本構造と、文字列を出力する方法を学びました。

- Javaでは、クラスの中にメソッドなどを定義する。
- `public class Main`は、`Main`というクラスの定義を表す。
- `main`メソッドは、基本的なJavaプログラムの実行開始地点になる。
- `System.out.println()`は文字列や数値を出力できる。
- `print()`は改行せず、`println()`は出力後に改行する。

今回学んだクラスと`main`メソッドの基本的な形は、今後のJava学習でも繰り返し登場します。

まずは自分でコードを書き、文字列を変更しながら出力結果を確認してみましょう。

## 参考資料

- [Oracle Java SE 17 API - PrintStream](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/PrintStream.html)
- [Dev.java - Classes and Objects](https://dev.java/learn/classes-objects/)
- [Dev.java - More on Classes](https://dev.java/learn/language/oop/classes-objects/more-on-classes/)

