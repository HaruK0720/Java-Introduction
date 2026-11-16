# Java入門】変数名の付け方を解説｜使える文字・予約語・キャメルケースの基本

<br>


## はじめに

Javaでは、変数に好きな名前を付けられます。しかし、どんな文字列でも使えるわけではありません。また、文法上は正しくても、何を表すのかわからない名前では、コードを読みにくくしてしまいます。

この記事ではJava 17を基準に、**変数名に使える文字・予約語・大文字小文字の区別**と、読みやすい名前を付けるための**キャメルケース**を解説します。

<br><br><br>

## 変数名は「識別子」の一種

変数名のように、プログラム内のものを区別する名前を**識別子（identifier）**といいます。

例えば、次の`studyMinutes`が変数名です。

```java
int studyMinutes = 45;
```

`int`は整数型、`45`は代入する値です。`studyMinutes`という名前から「学習した時間（分）」だと想像できます。

<br><br>

## Javaで使える文字・使えない文字

まずは一般的な英数字を使う場合のルールを確認しましょう。

| 変数名 | 使用可否 | 理由 |
| --- | --- | --- |
| `score` | ○ | 英字で始まる |
| `score2` | ○ | 2文字目以降に数字を使える |
| `_score` | ○ | アンダースコアから始められる |
| `$score` | ○ | ドル記号から始められる |
| `2score` | × | 数字からは始められない |
| `user name` | × | 空白を含む |
| `user-name` | × | `-`は名前に使えない |
| `_` | × | Java 17では単独の`_`は予約されている |

厳密にはJavaの識別子には、英字以外にも一定のUnicode文字を使用できます。例えば日本語の変数名も文法上は可能です。ただし、チームで読みやすく扱うため、通常は**意味のわかる英単語**を使うのがおすすめです。

`_score`や`$score`は文法上有効ですが、一般的な変数名では先頭の`_`や`$`を避ける慣習があります。

<br><br>

## 予約語は変数名に使えない

Javaでは、`int`・`class`・`public`・`if`など、言語として特別な役割を持つ**キーワード（予約語）**を変数名にできません。

```java
// いずれもコンパイルエラーになる例
// int class = 1;
// int public = 2;
// int if = 3;
```

また、`true`・`false`・`null`も変数名として使用できません。これらは厳密にはキーワードではなく、真偽値や`null`を表すリテラルです。

Java 17の`var`や`record`などは、すべての場面で禁止される予約語とは異なり、**一部の文脈で特別な意味を持つ識別子**です。初学者は混乱を避けるため、こうした名前も変数名に選ばない方がよいでしょう。

<br><br>

## 大文字と小文字は区別される

Javaでは、`score`と`Score`は**異なる名前**です。

```java
int score = 80;
int Score = 90;
```

これは文法上有効ですが、見間違えやすいため、同じ場所で似た名前を使うのは避けましょう。変数名は通常、小文字で始めます。

<br><br><br>

## キャメルケースで読みやすくする

複数の英単語から名前を作る場合は、最初を小文字にし、2語目以降の先頭だけを大文字にする**ローワーキャメルケース（lowerCamelCase）**が一般的です。

```java
int studyMinutes = 45;
int totalPrice = 1200;
String userName = "Taro";
```

`study_minutes`のようにアンダースコアで区切る方法は**スネークケース**と呼ばれますが、Javaの通常の変数名ではキャメルケースが広く使われます。

なお、`MAX_SIZE`のように大文字とアンダースコアを使う書き方は、主に**定数**の命名で用いる慣習です。定数は別の記事で詳しく扱います。

<br><br>

## 「良い名前」と「わかりにくい名前」を比較

文法上正しいだけでは、良い名前とは限りません。

| わかりにくい例 | 改善例 | 改善する理由 |
| --- | --- | --- |
| `a` | `age` | 年齢だとわかる |
| `n` | `studentCount` | 何の人数か伝わる |
| `data` | `userName` | 保存する情報が具体的 |
| `time` | `studyMinutes` | 用途と単位が明確 |
| `flag` | `isCompleted` | 真偽値の意味がわかる |

大切なのは、**変数の役割が名前から想像できること**です。長すぎる名前も読みにくくなるため、必要な情報だけを簡潔に表しましょう。

<br><br>

## サンプルコード：意味の伝わる名前を使う

**ファイル名：`NamingExample.java`**

```java
public class NamingExample {
    public static void main(String[] args) {
        String studentName = "Aoi";
        int studyMinutes = 45;
        int targetMinutes = 30;
        boolean isCompleted = studyMinutes >= targetMinutes;

        System.out.println("名前: " + studentName);
        System.out.println("学習時間: " + studyMinutes + "分");
        System.out.println("目標達成: " + isCompleted);
    }
}
```

**実行結果**

```text
名前: Aoi
学習時間: 45分
目標達成: true
```

`studyMinutes`と`targetMinutes`には単位が含まれているため、比較しているものがわかりやすくなっています。`isCompleted`は「達成済みか」を表す`boolean`型の変数なので、`true`や`false`が入ることも名前から想像できます。

<br><br><br>

## 練習問題

### 問題

次のプログラムは動きますが、変数名から用途がわかりにくくなっています。`a`・`b`・`c`を、それぞれ何を表すかわかる**キャメルケースの名前**に変更してください。

```java
public class NamingPractice {
    public static void main(String[] args) {
        int a = 120;
        int b = 3;
        int c = a * b;

        System.out.println("合計金額: " + c + "円");
    }
}
```

**期待する実行結果**

```text
合計金額: 360円
```

ヒント：`a`は商品の単価、`b`は購入個数、`c`は合計金額を表しています。

<br>

### 解答例

```java
public class NamingPractice {
    public static void main(String[] args) {
        int unitPrice = 120;
        int quantity = 3;
        int totalPrice = unitPrice * quantity;

        System.out.println("合計金額: " + totalPrice + "円");
    }
}
```

`unitPrice`は単価、`quantity`は数量、`totalPrice`は合計金額を意味します。計算結果は同じでも、**変数名を変えるだけで処理の意味を理解しやすくなります**。

<br><br>

## まとめ

- 変数名は識別子の一種で、数字から始めたり空白や`-`を含めたりできません。
- Javaの予約語や`true`・`false`・`null`は変数名に使用できません。
- 大文字と小文字は区別され、通常の変数名は小文字から始めます。
- 複数の単語は`studyMinutes`のような**ローワーキャメルケース**でつなぐのが一般的です。
- 文法上使える名前でも、**役割や単位が伝わる名前**を選ぶことが大切です。

<br><br>

## 参考資料

- [Java SE 17 言語仕様 - 3.8 Identifiers](https://docs.oracle.com/javase/specs/jls/se17/html/jls-3.html#jls-3.8)
- [Java SE 17 言語仕様 - 3.9 Keywords](https://docs.oracle.com/javase/specs/jls/se17/html/jls-3.html#jls-3.9)
- [Oracle - Code Conventions: Naming Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html)

