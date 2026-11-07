# 【Java入門】Javaの基本構造！クラスとメソッドの関係を理解する｜mainメソッドと処理の実行順序

<br>

## はじめに

Javaのコードを見ると、`class`や`main`、波括弧の`{ }`が何重にも並んでいます。

これらは適当に配置されているのではなく、**クラスの中にメソッドがあり、メソッドの中に処理を書く**という構造になっています。

この記事では、Java 17を前提に、クラス・メソッド・ステートメントの関係と、`main`メソッドから処理が実行される仕組みを解説します。

<br><br><br>

## Javaプログラムの基本構造

Javaのプログラムは、主に次の要素を組み合わせて作成します。

| 要素 | 役割 |
| --- | --- |
| クラス（class） | メソッドやデータなどをまとめる基本単位 |
| メソッド（method） | ひとまとまりの処理を定義するもの |
| ステートメント（statement／文） | 具体的な命令や処理を表すもの |

構造を簡単に表すと、次のようになります。

```text
クラス
├─ メソッド1
│  ├─ ステートメント1
│  └─ ステートメント2
└─ メソッド2
   ├─ ステートメント3
   └─ ステートメント4
```

これは構造のイメージであり、そのまま実行するJavaコードではありません。

**外側のクラスに複数のメソッドを定義でき、各メソッドの中に処理を書ける**という入れ子構造がポイントです。

<br>

### 波括弧とインデントの役割

Javaでは、波括弧`{ }`によってクラスやメソッドの範囲を表します。

また、インデント（字下げ）を使うと、どのコードがどの範囲に属するのかを読み取りやすくなります。インデント自体で構造が決まるわけではありません。

<br><br>

## mainメソッドは実行の開始地点

Java 17で、一般的なコマンドラインアプリケーションを`java`コマンドから起動する場合、起動対象のクラスには次の形式の`main`メソッドを用意します。

```java
public static void main(String[] args) {
    // ここから処理が始まる
}
```

`main`は、プログラムを起動したときに最初に呼び出されるメソッドです。

- `public`：外部から呼び出せることを示します。
- `static`：オブジェクトを作らずに呼び出せます。
- `void`：戻り値がないことを示します。
- `String[] args`：起動時に渡された文字列の引数を受け取ります。

なお、**プログラム全体に`main`メソッドが必ず1個しか置けないわけではありません**。複数のクラスに`main`を定義することもできますが、起動時には実行するクラスを選びます。

また、Javaを利用するすべての仕組みで`main`が必須というわけではありません。この記事では、基本的なコマンドラインアプリケーションを扱います。

<br><br><br>

## サンプルコード：2つのメソッドを使う

`main`メソッドのほかに、学習内容を表示する`showTopics`メソッドを定義します。

**ファイル名：`StudyPlan.java`**

```java
public class StudyPlan {
    public static void main(String[] args) {
        System.out.println("学習開始");
        showTopics();
        System.out.println("学習終了");
    }

    public static void showTopics() {
        System.out.println("1. クラス");
        System.out.println("2. メソッド");
    }
}
```

### 実行結果

```text
学習開始
1. クラス
2. メソッド
学習終了
```

<br>

### 処理が実行される順番

1. プログラムを起動すると、`main`メソッドが始まります。
2. `学習開始`を表示します。
3. `showTopics();`で別のメソッドを呼び出します。
4. `showTopics`内の2つのステートメントが実行されます。
5. 呼び出し元の`main`に戻り、`学習終了`を表示します。

```text
main開始
  ↓
「学習開始」を表示
  ↓
showTopics()を呼び出す
  ├─「1. クラス」を表示
  └─「2. メソッド」を表示
  ↓
mainに戻る
  ↓
「学習終了」を表示
```

ここで重要なのは、**メソッドを定義しただけでは、その中の処理は実行されない**ことです。`showTopics`は、`main`から呼び出されたときに実行されます。

今回は`main`から直接呼び出せるように、`showTopics`にも`static`を付けています。

<br><br>

## ステートメントとメソッド定義の違い

次の1行は、画面に文字列を表示する**ステートメント（文）**です。

```java
System.out.println("学習開始");
```

最後にセミコロン`;`が付いています。`showTopics();`もメソッドを呼び出すステートメントです。

一方、次のコードは**メソッドの定義**です。

```java
public static void showTopics() {
    System.out.println("1. クラス");
}
```

メソッドの定義では、`{ }`の中に処理を書きます。メソッド定義の閉じ波括弧`}`の後にセミコロンは不要です。

<br><br>

## よくある注意点

### ① メソッドを書く場所を間違えない

今回のようなメソッドは、**クラスの中、ほかのメソッドの外側**に定義します。`main`メソッドの内部に別のメソッドを定義することはできません。

### ② 定義した順番と実行順序は別

先ほどの例では、`showTopics`は`main`より下に書かれていますが、`showTopics();`を呼び出した時点で実行されます。

コードを上から並べた順に、すべてのメソッドが自動実行されるわけではありません。

### ③ クラス名とファイル名に注意

`public class StudyPlan`というトップレベルのクラスを定義した場合、ファイル名は`StudyPlan.java`にします。大文字と小文字も区別されます。

<br><br><br>

## 練習問題

### 問題

`WeeklySchedule`クラスを作成し、`main`メソッドから`printSchedule`メソッドを呼び出してください。

`printSchedule`メソッドには、月曜日と火曜日の学習予定を表示する2つのステートメントを書きます。また、`main`では呼び出しの前後に開始・終了のメッセージを表示してください。

**期待する実行結果**

```text
予定を表示します
月曜: Java
火曜: SQL
表示終了
```

**ヒント：** `main`と`printSchedule`は同じクラスの中に別々に定義し、`main`内で`printSchedule();`と書いて呼び出します。

<br>

### 解答例

```java
public class WeeklySchedule {
    public static void main(String[] args) {
        System.out.println("予定を表示します");
        printSchedule();
        System.out.println("表示終了");
    }

    public static void printSchedule() {
        System.out.println("月曜: Java");
        System.out.println("火曜: SQL");
    }
}
```

### 解答の解説

最初に`main`の1行目が実行され、続いて`printSchedule()`が呼び出されます。

予定を2行表示したら`main`に戻り、最後の`表示終了`が出力されます。1つのクラスに複数のメソッドを定義し、処理を分担させる例です。

<br><br>

## まとめ

- Javaでは、**クラスの中にメソッドを定義し、メソッドの中にステートメントを書く**のが基本です。
- 波括弧`{ }`で範囲を区切り、インデントで構造を読みやすくします。
- Java 17の基本的なコマンドラインアプリケーションは、`main`メソッドから処理を開始します。
- ほかのメソッドは、呼び出されることで処理を実行します。
- **メソッドの定義順と実行順序は同じとは限りません**。

コードを読むときは、まず`main`を探し、そこからどのメソッドが呼び出されるかを追ってみましょう。

<br><br>

## 参考資料

- [Oracle Java SE 17 - javaコマンド](https://docs.oracle.com/javase/jp/17/docs/specs/man/java.html)
- [Dev.java - Defining Methods](https://dev.java/learn/language/oop/classes-objects/defining-methods/)
- [Oracle Java Tutorials - Expressions, Statements, and Blocks](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/expressions.html)（Java 8向け教材ですが、ここで紹介した文・ブロックの基本はJava 17にも共通です）

