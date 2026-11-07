# 【Java入門】読みやすいコードの書き方｜インデントと波括弧の整え方

<br>

## はじめに

Javaのコードでは、行の先頭に空白を入れて、クラスやメソッドの中身を少し右にずらして書きます。この字下げを**インデント**と呼びます。

インデントをそろえると、コードのまとまりや処理の流れが読み取りやすくなります。この記事では、Java 17を前提に、基本的な字下げの方法と波括弧`{ }`との違いを学びます。

<br><br><br>

## インデントは何のためにある？

**インデント**とは、行頭にスペースやタブを入れて、コードを右にずらすことです。

Javaでは、クラスやメソッド、`if`などの処理の範囲を**ブロック**と呼び、通常は波括弧`{ }`で囲みます。インデントは、その入れ子構造を見やすくするために使います。

例えば、次のように、内側へ入るたびに字下げを1段階増やします。

```text
クラス
    メソッド
        if文
            実行する処理
```

インデントは、書いた人だけでなく、あとからコードを読む人が構造を把握するためにも役立ちます。

<br><br>

## 基本の付け方をコードで確認する

この記事では、**1段階につき半角スペース4個**を使います。

**ファイル名：`IndentExample.java`**

```java
public class IndentExample {
    public static void main(String[] args) {
        int score = 85;

        if (score >= 80) {
            System.out.println("合格");
        }

        System.out.println("判定終了");
    }
}
```

**実行結果**

```text
合格
判定終了
```

<br>

### インデントを増やす場所

- `class`の内側：スペース4個
- `main`メソッドの内側：スペース8個
- `if`ブロックの内側：スペース12個

`score >= 80`は「点数が80以上か」を調べる条件です。今回は`85`なので、`合格`が表示されます。その後、`if`の外にある`判定終了`も表示されます。

閉じ波括弧`}`は、対応する開始位置に戻してそろえます。こうすると、どこからどこまでが同じブロックなのか一目でわかります。

<br><br><br>

## インデントがずれていても実行できる？

先ほどのプログラムを、字下げなしで書いてみます。

```java
public class IndentExample {
public static void main(String[] args) {
int score = 85;
if (score >= 80) {
System.out.println("合格");
}
System.out.println("判定終了");
}
}
```

このコードも、先ほどと同じようにコンパイル・実行でき、同じ結果になります。しかし、クラス・メソッド・`if`の範囲が読み取りにくくなっています。

**Javaでは、通常のコードの行頭の空白そのものではなく、波括弧などの構文によって処理の範囲が決まります。** そのため、見た目を整えるインデントと、構文上の区切りを混同しないことが大切です。

※文字列や複数行のテキストブロック内の空白など、空白の位置に意味がある場合は別です。

<br><br>

## 注意：インデントと波括弧は別物

次のコードでは、`if`の条件が成立しない場合でも`判定終了`が表示されます。

**ファイル名：`IndentPitfall.java`**

```java
public class IndentPitfall {
    public static void main(String[] args) {
        int score = 60;
        if (score >= 80)
            System.out.println("合格");
            System.out.println("判定終了");
    }
}
```

**実行結果**

```text
判定終了
```

波括弧を省略した`if`では、直後の**1つの文だけ**が条件付きになります。2つ目の`println()`は字下げされていても`if`の外側にあるため、実行されます。

誤解を防ぐため、1行だけの条件分岐でも波括弧を付けて書くのがおすすめです。

```java
if (score >= 80) {
    System.out.println("合格");
}
System.out.println("判定終了");
```

<br><br>

## スペースとタブはどちらを使う？

インデントには主に**スペース**と**タブ**が使われます。

| 方法 | 特徴 |
| --- | --- |
| スペース | 字下げの幅を明確にそろえやすい |
| タブ | エディタの設定によって表示幅が変わる |

「インデントは必ず4スペース」というJavaの文法上の決まりはありません。例えば、[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)では**2スペース**を採用しています。

学習時は4スペースなどに統一し、チーム開発では**プロジェクトのコーディング規約**に合わせましょう。スペースとタブを混ぜないことも重要です。

また、多くのコードエディタには自動整形（フォーマット）機能があります。手作業で空白を数えるよりも、設定したルールでコードを整えると効率的です。

<br><br><br>

## 練習問題

### 問題

次のコードは、インデントがすべてなくなっています。**1段階につき半角スペース4個**で、読みやすく整形してください。

波括弧や処理の内容は変更しないでください。

```java
public class StudyTime {
public static void main(String[] args) {
int minutes = 45;
if (minutes >= 30) {
System.out.println("目標達成");
}
System.out.println("記録完了");
}
}
```

**期待する実行結果**

```text
目標達成
記録完了
```

ヒント：`class`→`main`→`if`と内側へ進むたびに、字下げを1段階増やします。

<br>

### 解答例

```java
public class StudyTime {
    public static void main(String[] args) {
        int minutes = 45;
        if (minutes >= 30) {
            System.out.println("目標達成");
        }
        System.out.println("記録完了");
    }
}
```

`if`の内部にある`目標達成`だけをさらに1段階下げ、`if`の外にある`記録完了`は`int minutes`と同じ位置にそろえます。字下げを直しても、処理内容と実行結果は変わりません。

<br><br>

## まとめ

- インデントは**行頭の字下げ**で、コードの入れ子構造を見やすくするものです。
- クラス・メソッド・`if`などの内側では、字下げを1段階増やします。
- Javaの処理範囲は、通常、インデントではなく波括弧などの構文で決まります。
- スペースの個数は統一し、チームではコーディング規約に合わせます。
- 自動整形を活用すると、読みやすいコードを保ちやすくなります。

<br><br>

## 参考資料

- [Java SE 17 言語仕様 - Lexical Structure（字句構造）](https://docs.oracle.com/javase/specs/jls/se17/html/jls-3.html)
- [Google Java Style Guide - Formatting](https://google.github.io/styleguide/javaguide.html#s4-formatting)

