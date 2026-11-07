# 【Java入門】よくある間違い7選！コンパイルエラーの原因と直し方を解説

## はじめに

Javaを学び始めたばかりの頃は、コードを書いてもエラーが発生して、プログラムが動かないことがあります。

例えば、セミコロン（`;`）を忘れたり、大文字と小文字を間違えたりするだけでも、正しく動作しなくなる場合があります。

この記事では、**Java初心者がよく遭遇する7つの間違いと、その原因・修正方法**を解説します。

- コンパイルエラーとその他の間違いの違い
- Javaでよくある7つの間違い
- エラーメッセージの確認方法
- 間違ったコードを修正する練習問題

## Javaのエラーとは？

まず、次のJavaプログラムを見てみましょう。

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

このプログラムは、`Hello World`という文字列を画面に表示します。

```text
Hello World
```

Javaでは、ソースコードを実行可能な形式に変換する**コンパイル**という処理を行います。<br>
その際、コードの書き方に誤りがあると、コンパイラがエラーを検出します。

また、コンパイルに成功しても、プログラムの起動時や実行中に問題が発生することがあります。

### 間違いの種類

初心者が遭遇する問題は、大きく次のように整理できます。

| 種類 | 内容 |
| --- | --- |
| コンパイルエラー | 文法などの問題でコンパイルできない |
| 起動・実行時のエラー | コンパイル後、起動時や実行中に問題が発生する |
| 論理的な間違い | プログラムは動くが、期待する結果にならない |

**エラーが出ないからといって、必ずしも正しいプログラムとは限りません。**

それぞれの違いを意識しながら、よくある間違いを確認していきましょう。

## Javaプログラムのよくある間違い7選

### ① セミコロン（;）を忘れる

Javaでは、通常、文の終わりにセミコロン（`;`）を記述します。

**間違った例（mainメソッド内の抜粋）**

```java
System.out.println("Hello World")
```

このコードでは、文の最後にセミコロンがありません。<br>
そのため、コンパイルエラーが発生します。

**正しい例**

```java
System.out.println("Hello World");
```

なお、クラスやメソッドを定義する波括弧（`{ }`）の後には、通常セミコロンは必要ありません。

### ② 文字列をダブルクォーテーションで囲まない

Javaでは、文字列を扱うときにダブルクォーテーション（`"`）を使用します。

**間違った例**

```java
System.out.println(Hello);
```

このコードでは、`Hello`が文字列ではなく、変数などの名前として解釈されます。

`Hello`という変数などが定義されていなければ、コンパイルエラーになります。

**正しい例**

```java
System.out.println("Hello");
```

文字列として出力したい場合は、ダブルクォーテーションで囲みましょう。

### ③ 大文字と小文字を間違える

Javaでは、**大文字と小文字が区別されます。**

例えば、次のコードは誤りです。

```java
system.out.println("Hello");
```

正しくは次のように記述します。

```java
System.out.println("Hello");
```

`System`と`system`は、Javaでは異なる名前として扱われます。

同様に、`println`を`Println`と書いても正しく動作しません。<br>
クラス名やメソッド名は、大文字と小文字を含めて正確に記述する必要があります。

### ④ 波括弧 { } の対応を間違える

Javaでは、クラスやメソッドの範囲を波括弧（`{ }`）で表します。

**間違った例**

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
}
```

このコードでは、クラスを閉じるための`}`が不足しています。

**正しい例**

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

外側の波括弧はクラスの範囲、内側の波括弧は`main`メソッドの範囲を表します。

インデント（字下げ）をそろえると、対応関係がわかりやすくなります。

### ⑤ mainメソッドの名前を間違える

Javaの基本的なプログラムでは、`main`メソッドが処理の開始地点になります。

**間違った例**

```java
public class Main {
    public static void Main(String[] args) {
        System.out.println("Hello");
    }
}
```

このコードでは、メソッド名が`Main`になっています。

Javaでは`main`と`Main`は異なる名前です。

このコード自体はコンパイルできますが、通常の`java Main`という起動方法では、必要な`main`メソッドが見つからず、起動できません。

**正しい例**

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

`public static void main(String[] args)`という基本的な形を覚えておきましょう。

### ⑥ クラス名とファイル名が一致していない

Javaでは、`public`を付けたトップレベルのクラス名と、ソースファイル名を一致させる必要があります。

例えば、次のコードを`Main.java`というファイルに保存したとします。

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

この場合、クラス名が`Hello`なのに、ファイル名が`Main.java`になっているため、コンパイルエラーになります。

修正方法は、次のいずれかです。

- ファイル名を`Hello.java`に変更する。
- クラス名を`Main`に変更する。

クラス名とファイル名を変更するときは、大文字と小文字にも注意しましょう。

### ⑦ print()とprintln()を間違える

最後は、コンパイルエラーにはならないものの、期待と異なる結果になる例です。

次のコードを見てみましょう。

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("Hello");
        System.out.println("Java");
    }
}
```

出力結果は次のとおりです。

```text
HelloJava
```

`print()`は出力後に改行しないため、`Java`が`Hello`の直後に表示されます。

`Hello Java`と表示したい場合は、次のようにスペースを追加します。

```java
System.out.print("Hello ");
System.out.println("Java");
```

**出力結果**

```text
Hello Java
```

このように、プログラムが正常に動いても、意図した出力にならないことがあります。

## エラーが発生したときの対処方法

エラーが発生した場合は、表示されたメッセージを確認することが重要です。

例えば、`Main.java`をコンパイルする場合、次のコマンドを使用できます。

```text
javac Main.java
```

コンパイル時に問題が見つかると、エラーメッセージが表示されます。

### エラーメッセージの見方

例えば、セミコロンを忘れた場合、次のようなメッセージが表示されることがあります。

```text
error: ';' expected
```

これは、セミコロンが必要な場所にないことを示しています。

ただし、エラーメッセージの内容や表示位置は、Javaのバージョンやコードの状態によって異なります。

### エラーを修正する手順

1. **エラーメッセージを確認する**：何が問題なのかを調べる。
2. **指摘された行とその周辺を見る**：セミコロンや波括弧の不足などを確認する。
3. **コードを修正する**：原因と思われる部分を書き直す。
4. **再度コンパイル・実行する**：問題が解消されたか確認する。

エラーが複数表示されても、必ずしもすべてが別々の原因とは限りません。<br>
まずは最初のエラーから確認し、修正するたびに結果を確かめると原因を特定しやすくなります。

## 練習問題

これまで学んだ内容を使って、間違ったJavaプログラムを修正してみましょう。

### 問題

次のコードには、**4か所の間違い**があります。

ファイル名を`Main.java`として、正しく実行できるように修正してください。

```java
public class Main {
    public static void Main(String[] args) {
        system.out.println("Hello Java")
        System.out.println(Java);
    }
}
```

**期待する出力結果**

```text
Hello Java
Java
```

<details>
<summary>ヒントを見る</summary>

以下の4点を確認してみましょう。

- メソッド名の大文字と小文字
- `System`の書き方
- 文の終わり
- 文字列の囲み方

</details>

### 解答例

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Java");
        System.out.println("Java");
    }
}
```

### 解答の解説

修正したのは次の4か所です。

| 間違い | 修正 |
| --- | --- |
| `Main`メソッド | `main`に変更 |
| `system` | `System`に変更 |
| セミコロンの不足 | `;`を追加 |
| `Java` | `"Java"`に変更 |

これらを修正することで、コンパイルと実行が正常に行われ、期待した2行が表示されます。

## まとめ

今回は、Javaプログラムでよくある間違いと、その対処方法を学びました。

- 文の終わりのセミコロンを忘れない。
- 文字列はダブルクォーテーションで囲む。
- 大文字と小文字、波括弧の対応に注意する。
- `main`メソッドやクラス名・ファイル名を正しく記述する。
- エラーがなくても、出力結果が正しいか確認する。

エラーが発生したときは、表示されたメッセージを読み、原因を一つずつ確認することが大切です。

間違いを修正する経験を重ねることで、Javaの構文への理解も深まっていきます。

## 参考資料

- [Dev.java - Getting Started with Java](https://dev.java/learn/getting-started/)
- [Oracle Java SE 17 - javacコマンド](https://docs.oracle.com/en/java/javase/17/docs/specs/man/javac.html)
- [Oracle Java SE 17 - javaコマンド](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html)
- [Oracle Java SE 17 API - PrintStream](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/PrintStream.html)

