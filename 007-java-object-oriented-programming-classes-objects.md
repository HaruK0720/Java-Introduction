# 【Java入門】オブジェクト指向とは？クラスとオブジェクトを身近な例で理解する

<br>

## はじめに

図書館で本を借りる、ネットショップで商品を注文する、学校で出席を記録する。こうした現実世界の活動は、コンピュータ上のプログラムでも扱えます。

その際に役立つ考え方の一つが、**オブジェクト指向プログラミング**です。この記事ではJava 17を使い、「本の貸出」を例にオブジェクト・クラス・状態・振る舞いの関係を解説します。

<br><br><br>

## 現実世界の活動をプログラムで表す

例えば、図書館の貸出管理システムでは、「どの本があるか」「その本は貸出中か」「貸し出したら状態がどう変わるか」を扱う必要があります。

現実の本をそのままコンピュータに入れるのではありません。必要な情報と操作を選び、**現実の仕組みをモデル（簡略化した表現）としてプログラムに置き換える**のです。

本なら、次のように整理できます。

| 観点 | 図書館の本の例 |
| --- | --- |
| 状態（データ） | タイトル、貸出中かどうか |
| 振る舞い（操作） | 貸し出す、返却する、状態を表示する |

すべてのJavaプログラムが現実世界の物を再現するわけではありませんが、業務や生活の仕組みを表現する場面では、この考え方が役立ちます。

<br><br>

## オブジェクト指向とは？

**オブジェクト指向プログラミング**は、データとそのデータに関係する操作を、**オブジェクト**という単位でまとめてプログラムを組み立てる考え方です。

オブジェクトには、主に次の2つの側面があります。

- **状態（state）**：そのオブジェクトが持っている情報。Javaでは主にフィールド（変数）で表します。
- **振る舞い（behavior）**：そのオブジェクトが行う処理。Javaではメソッドで表します。

### クラスとオブジェクトの違い

Javaでは、一般的に**クラスを設計図として定義し、そのクラスからオブジェクトを作ります**。作成されたオブジェクトは「インスタンス」とも呼ばれます。

```text
Bookクラス（本の設計図）
   ├─ javaBook（「Java入門」の本）
   └─ designBook（「デザイン基礎」の本）
```

同じ`Book`クラスから作ったオブジェクトでも、それぞれ別の状態を持てます。例えば、片方だけを貸出中にすることができます。

<br><br><br>

## Javaで「本の貸出」を表してみる

**ファイル名：`LibraryApp.java`**

```java
public class LibraryApp {
    public static void main(String[] args) {
        Book javaBook = new Book("Java入門");
        Book designBook = new Book("デザイン基礎");

        javaBook.showStatus();
        designBook.showStatus();

        javaBook.borrow();

        javaBook.showStatus();
        designBook.showStatus();
    }
}

class Book {
    String title;
    boolean borrowed = false;

    Book(String name) {
        title = name;
    }

    void borrow() {
        borrowed = true;
    }

    void showStatus() {
        if (borrowed) {
            System.out.println(title + "：貸出中");
        } else {
            System.out.println(title + "：貸出可能");
        }
    }
}
```

**実行結果**

```text
Java入門：貸出可能
デザイン基礎：貸出可能
Java入門：貸出中
デザイン基礎：貸出可能
```

<br>

### コードの動作を確認する

1. `class Book`で、本に必要なデータと操作を定義します。
2. `title`は本のタイトル、`borrowed`は貸出中かどうかを表す**フィールド**です。`boolean`には`true`か`false`が入ります。
3. `new Book("Java入門")`でオブジェクトを作ります。`Book(String name)`は、作成時にタイトルを設定する**コンストラクタ**です。
4. `javaBook.borrow()`で、その本の`borrowed`を`true`に変更します。
5. `showStatus()`は状態に応じて表示を切り替えます。

重要なのは、**`javaBook`を貸し出しても、`designBook`の状態は変わらない**点です。同じ設計図から作られていても、オブジェクトごとに状態を管理できます。

なお、この例では学習のため、貸出可能かどうかの厳密なチェックなどは省略しています。

<br><br>

## オブジェクト指向を使う利点と注意点

データと関連する処理をまとめると、「本の状態を変更する処理は`Book`にある」というように、**役割ごとのまとまり**を作れます。同じクラスから複数のオブジェクトを作れる点も便利です。

ただし、オブジェクト指向は、現実世界を完全に再現するための仕組みではありません。必要な特徴だけを取り出してモデル化します。また、プログラムに登場するオブジェクトは、本や人などの物理的なものだけでなく、注文・予約・処理結果などの概念を表す場合もあります。

<br><br><br>

## 練習問題

### 問題

先ほどの`Book`クラスに、**本を返却する`returnBook()`メソッド**を追加してください。

`javaBook`を貸し出して状態を表示した後、返却してもう一度状態を表示するプログラムにしましょう。

**期待する実行結果**

```text
Java入門：貸出中
Java入門：貸出可能
```

ヒント：貸出中を表す`borrowed`を、返却時には`false`に戻します。

<br>

### 解答例

**ファイル名：`LibraryApp.java`**

```java
public class LibraryApp {
    public static void main(String[] args) {
        Book javaBook = new Book("Java入門");

        javaBook.borrow();
        javaBook.showStatus();

        javaBook.returnBook();
        javaBook.showStatus();
    }
}

class Book {
    String title;
    boolean borrowed = false;

    Book(String name) {
        title = name;
    }

    void borrow() {
        borrowed = true;
    }

    void returnBook() {
        borrowed = false;
    }

    void showStatus() {
        if (borrowed) {
            System.out.println(title + "：貸出中");
        } else {
            System.out.println(title + "：貸出可能");
        }
    }
}
```

`returnBook()`はオブジェクトの**状態を変更する振る舞い**です。返却後は同じ`javaBook`の状態が変わるため、`showStatus()`の表示結果も変わります。

<br><br>

## まとめ

- プログラムでは、現実の活動に必要な情報や操作を取り出して表現できます。
- **オブジェクト指向**は、関係する状態と振る舞いをオブジェクトという単位で扱う考え方です。
- **クラス**は設計図、**オブジェクト**はクラスから作られた実体です。
- 同じクラスから作ったオブジェクトでも、それぞれ独立した状態を持てます。
- Javaでは、フィールドで状態を、メソッドで振る舞いを表します。

<br><br>

## 参考資料

- [Dev.java - Objects, Classes, Interfaces, Packages, and Inheritance](https://dev.java/learn/oop/)
- [Dev.java - Classes and Objects](https://dev.java/learn/language/oop/classes-objects/)
- [Oracle Java Tutorials - What Is an Object?](https://docs.oracle.com/javase/tutorial/java/concepts/object.html)（Java 8向け教材ですが、オブジェクトの基本概念はJava 17にも共通です）

