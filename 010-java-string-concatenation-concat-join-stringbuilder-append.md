# 【Java入門】文字列をつなぐ5つの方法｜+・concat()・join()・StringBuilderの使い分け

<br>

## はじめに

Javaでは、名前とメッセージを組み合わせたり、複数の単語を区切り文字でつないだりして、1つの文字列を作ることがあります。これを**文字列結合（文字列連結）**と呼びます。

前回扱った`+`演算子のほかにも、`String`クラスのメソッドや`StringBuilder`を使う方法があります。この記事では、Java 17で利用できる5つの方法と、場面に応じた使い分けを学びます。

<br><br><br>

## 文字列をつなぐ5つの方法

| 方法 | 向いている場面 |
| --- | --- |
| `+` | 短い文字列を手軽につなぐ |
| `concat()` | 文字列の末尾に別の文字列をつなぐ |
| `String.join()` | 複数の文字列を区切り文字でつなぐ |
| `StringBuilder.append()` | 文字列を段階的・繰り返し組み立てる |
| `String.format()` | 決まった形式の文章に値を埋め込む |

`String.format()`は厳密には「文字列の書式設定」のためのメソッドですが、複数の値を組み合わせた文章を作るときにも役立ちます。

<br><br>

## ① `+`演算子：手軽に文字列をつなぐ

```java
String name = "さくら";
int score = 85;
String message = name + "さんの点数は" + score + "点";
```

`+`は、文字列同士だけでなく、文字列と数値もつなげられます。この例では数値の`85`が文字列表現に変換されます。

短いメッセージを作るなら、まずはこの方法がわかりやすいでしょう。なお、数値の足し算も含む場合は、`"合計: " + (10 + 5)`のように括弧で計算順序を明確にします。

<br><br>

## ② `concat()`：文字列の末尾に追加する

```java
String text = "Java";
String result = text.concat("入門");
```

`concat()`は、**呼び出し元の文字列の末尾に、指定した文字列をつないだ結果を返す**メソッドです。

ここで大切なのは、`String`は一度作ると内容を変更できない（**不変／イミュータブル**）という点です。`text.concat("入門")`だけを実行しても、元の`text`が`"Java入門"`に変わるわけではありません。結合結果を使うには、戻り値を受け取ります。

また、`concat()`の引数は`String`です。`+`のように数値をそのまま渡すことはできません。

<br><br>

## ③ `String.join()`：区切り文字を入れてつなぐ

```java
String subjects = String.join("・", "Java", "SQL", "HTML");
```

結果は`Java・SQL・HTML`です。最初の`"・"`が**区切り文字**で、その後の文字列の間に自動的に挿入されます。

`String.join()`は、文字列の配列やリストを結合する場合にも使えます。科目名やタグを一覧にするときに便利です。

<br><br>

## ④ `StringBuilder.append()`：文字列を組み立てる

```java
StringBuilder builder = new StringBuilder();
builder.append("今日の学習: ");
builder.append("Java");
builder.append(" / ").append(30).append("分");
String result = builder.toString();
```

`append()`は`StringBuilder`が持つ文字列の末尾に、値を追加します。`toString()`で完成した内容を`String`として取得できます。

`String`とは異なり、`StringBuilder`は**同じオブジェクトの内容を変更しながら**文字列を作れます。特にループなどで何度も追加する場合に便利です。ただし、短い結合でも常に`+`より速いと決めつける必要はありません。

<br><br>

## ⑤ `String.format()`：文章に値を埋め込む

```java
String name = "さくら";
int score = 85;
String message = String.format("%sさんの点数は%d点", name, score);
```

`%s`は文字列などを、`%d`は整数を埋め込むための**書式指定子**です。メッセージの形が決まっている場合に、文字列と値の対応が読み取りやすくなります。

<br><br><br>

## サンプルコードで5つを比較する

**ファイル名：`StringCombineExample.java`**

```java
public class StringCombineExample {
    public static void main(String[] args) {
        String name = "さくら";
        int score = 85;

        String plus = name + "さんの点数は" + score + "点";
        String concat = "Java".concat("入門");
        String join = String.join("・", "Java", "SQL", "HTML");

        StringBuilder builder = new StringBuilder();
        builder.append("今日の学習: ");
        builder.append("Java");
        builder.append(" / ").append(30).append("分");

        String formatted = String.format("%sさんの点数は%d点", name, score);

        System.out.println("+: " + plus);
        System.out.println("concat: " + concat);
        System.out.println("join: " + join);
        System.out.println("builder: " + builder.toString());
        System.out.println("format: " + formatted);
    }
}
```

保存したフォルダで、次のコマンドからコンパイル・実行できます。

```bash
javac -encoding UTF-8 StringCombineExample.java
java StringCombineExample
```

**実行結果**

```text
+: さくらさんの点数は85点
concat: Java入門
join: Java・SQL・HTML
builder: 今日の学習: Java / 30分
format: さくらさんの点数は85点
```

`+`と`String.format()`は同じ文章を作っていますが、前者は値を順につなぎ、後者は文章の指定位置に値を埋め込みます。

`concat()`と`join()`は、文字列をつなぐ点では似ていますが、区切り文字を自動で入れたいなら`join()`が適しています。`StringBuilder`は`append()`を呼ぶたびに内容が増えていきます。

<br><br>

## 使い分けと注意点

**選び方の目安**は、短い結合なら`+`、区切り付きの一覧なら`String.join()`、繰り返し追加するなら`StringBuilder`、書式が決まった文章なら`String.format()`です。`concat()`は、文字列に別の文字列を追加するシンプルな選択肢です。

また、次の違いを覚えておきましょう。

- `String`は不変なので、`concat()`の結果を使うには戻り値を受け取ります。
- `StringBuilder`は可変で、`append()`が同じオブジェクトを変更します。
- `String.join()`は区切り文字を**要素と要素の間**に入れます。末尾には自動で追加しません。
- 数値を含む文字列結合では、`+`による加算と連結を混同しないようにします。

<br><br><br>

## 練習問題

### 問題

次の3科目を、`String.join()`を使って` / `でつないでください。その後、`+`演算子を使って、名前を付けたメッセージとして表示しましょう。

- 名前：`Aoi`
- 科目：`Java`、`SQL`、`CSS`

**期待する実行結果**

```text
Aoiさんの学習科目: Java / SQL / CSS
```

ヒント：`String.join(" / ", ...)`で科目をつないでから、名前と結合します。

<br>

### 解答例

**ファイル名：`StudySubjects.java`**

```java
public class StudySubjects {
    public static void main(String[] args) {
        String name = "Aoi";
        String subjects = String.join(" / ", "Java", "SQL", "CSS");

        String message = name + "さんの学習科目: " + subjects;
        System.out.println(message);
    }
}
```

まず`String.join()`で3科目の間に` / `を入れ、1つの文字列を作ります。続いて`+`演算子で名前と説明文をつなぐことで、期待したメッセージになります。

<br><br>

## まとめ

- `+`は短い文字列の結合に手軽に使えます。
- `concat()`は文字列の末尾に追加した**新しい結果**を返します。
- `String.join()`は複数の文字列を区切り文字付きで結合します。
- `StringBuilder.append()`は文字列を段階的・繰り返し組み立てるときに便利です。
- `String.format()`は決まった形式の文章に値を埋め込む方法です。

文字列結合には複数の選択肢があります。まずは`+`と`String.join()`を使ってみて、用途に応じてほかの方法も選べるようにしましょう。

<br><br>

## 参考資料

- [Java SE 17 言語仕様 - 文字列連結演算子`+`](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.18.1)
- [Java SE 17 API - String（concat・join・format）](https://docs.oracle.com/javase/jp/17/docs/api/java.base/java/lang/String.html)
- [Java SE 17 API - StringBuilder（append・toString）](https://docs.oracle.com/javase/jp/17/docs/api/java.base/java/lang/StringBuilder.html)

