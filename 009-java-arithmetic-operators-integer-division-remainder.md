# 【Java入門】四則演算と余りの計算｜整数の割り算・優先順位の注意点も解説

<br>

## はじめに

Javaでは、足し算・引き算などの計算を**算術演算子**で表します。普段の計算と似ていますが、整数同士を割ったときの結果や、文字列と数値を足すときの動作には注意が必要です。

この記事ではJava 17を基準に、5つの基本的な演算子と、計算結果が予想と違ってしまう原因をサンプルコードで確認します。

<br><br><br>

## 基本の5つの算術演算子

**演算子**は、値を使って計算などを行うための記号です。算術演算では、次の5つをよく使います。

| 演算子 | 意味 | 例 | 結果 |
| --- | --- | --- | --- |
| `+` | 足し算（加算） | `17 + 5` | `22` |
| `-` | 引き算（減算） | `17 - 5` | `12` |
| `*` | 掛け算（乗算） | `17 * 5` | `85` |
| `/` | 割り算（除算） | `17 / 5` | `3` |
| `%` | 割り算の余り（剰余） | `17 % 5` | `2` |

掛け算には`×`ではなく`*`、割り算には`÷`ではなく`/`を使います。`%`は「パーセント」ではなく、**割り算の余り**を求める演算子です。

<br><br>

## サンプルコードで動きを確認する

**ファイル名：`ArithmeticExample.java`**

```java
public class ArithmeticExample {
    public static void main(String[] args) {
        int a = 17;
        int b = 5;

        System.out.println("足し算: " + (a + b));
        System.out.println("引き算: " + (a - b));
        System.out.println("掛け算: " + (a * b));
        System.out.println("割り算: " + (a / b));
        System.out.println("余り: " + (a % b));
    }
}
```

保存したフォルダで、次のコマンドからコンパイル・実行できます。

```bash
javac -encoding UTF-8 ArithmeticExample.java
java ArithmeticExample
```

**実行結果**

```text
足し算: 22
引き算: 12
掛け算: 85
割り算: 3
余り: 2
```

`int`は整数を扱うデータ型です。`17 / 5`では、17を5で割った**商の整数部分に当たる3**が得られます。`17 % 5`では、5を3回引いた残りの`2`が得られます。

<br><br><br>

## 整数の割り算と小数の割り算は違う

Javaでは、両方の値が整数型なら、割り算の結果も整数になります。小数部分は**0に向かって切り捨て**られます（四捨五入ではありません）。

| 式 | 結果 | 理由 |
| --- | --- | --- |
| `10 / 4` | `2` | 整数同士の割り算 |
| `10.0 / 4` | `2.5` | 小数を含む割り算 |
| `(double) 10 / 4` | `2.5` | 一方を`double`に変換 |
| `-10 / 4` | `-2` | 0に向かって切り捨て |

`double`は小数を扱うデータ型です。小数の結果が必要なときは、**割る前に少なくとも一方の値を`double`にする**ことが大切です。

```java
public class DivisionExample {
    public static void main(String[] args) {
        int total = 10;
        int count = 4;

        System.out.println(total / count);
        System.out.println((double) total / count);
    }
}
```

**実行結果**

```text
2
2.5
```

なお、`double result = total / count;`と書いても、先に整数の割り算が行われるため、結果は`2.0`です。変数の型を`double`にするだけでは、小数部分は復元されません。

<br><br>

## 計算の優先順位と括弧

算術演算子を組み合わせた式では、基本的に`*`・`/`・`%`が`+`・`-`より優先されます。同じ優先順位の演算子が連続する場合は、左から順にまとまります。

```java
public class OrderExample {
    public static void main(String[] args) {
        System.out.println(8 + 3 * 2);
        System.out.println((8 + 3) * 2);
        System.out.println(20 / 5 * 2);
    }
}
```

**実行結果**

```text
14
22
8
```

`8 + 3 * 2`では先に`3 * 2`を計算します。一方、`(8 + 3) * 2`では括弧の中を先に計算します。

**読み手に計算順序を明確に伝えたいときは、括弧を使う**とわかりやすくなります。

<br><br>

## よくある間違い

### ① 文字列と数値の`+`を混同する

`+`には、数値の足し算だけでなく**文字列を連結する役割**もあります。

```java
System.out.println("合計: " + 10 + 5);   // 合計: 105
System.out.println("合計: " + (10 + 5)); // 合計: 15
```

最初の行では、文字列に数値を順番につなげます。計算してから表示したい場合は、`(10 + 5)`のように括弧で囲みます。

<br>

### ② 0で割る

整数の`/`や`%`で右側の値が`0`の場合は、実行時に`ArithmeticException`が発生します。

```java
int divisor = 0;
// System.out.println(10 / divisor); // 実行すると例外が発生
```

一方、小数型の演算では`10.0 / 0.0`の結果は`Infinity`になります。このように、同じ`/`でもデータ型によって動作が異なります。

<br>

### ③ 余りはいつも正になると思う

Javaでは、負の整数を使った剰余は負になる場合があります。例えば、`-10 % 3`の結果は`-1`です。余りの符号にも注意しましょう。

<br><br><br>

## 練習問題

### 問題

23個のお菓子を4人で均等に分けます。**1人が受け取る個数**と**余る個数**を`/`と`%`で計算して表示してください。

**期待する実行結果**

```text
1人あたり: 5個
余り: 3個
```

ヒント：個数を整数の変数で用意し、割り算で1人分、剰余で余りを求めます。

<br>

### 解答例

**ファイル名：`SnackShare.java`**

```java
public class SnackShare {
    public static void main(String[] args) {
        int snacks = 23;
        int people = 4;

        int perPerson = snacks / people;
        int remainder = snacks % people;

        System.out.println("1人あたり: " + perPerson + "個");
        System.out.println("余り: " + remainder + "個");
    }
}
```

`23 / 4`は`5`、`23 % 4`は`3`です。実際に`5 × 4 + 3 = 23`となり、すべてのお菓子の個数と一致します。**まとまった数に分けて余りを調べる処理**で、`/`と`%`はよく一緒に使われます。

<br><br>

## まとめ

- `+`・`-`・`*`・`/`・`%`で四則演算と余りを計算できます。
- **整数同士の割り算では小数部分が切り捨てられます**。小数が必要なら演算前に`double`を使います。
- `*`・`/`・`%`は`+`・`-`より優先され、括弧で計算順序を変えられます。
- `+`は文字列連結にも使われるため、計算を先に行うときは括弧が便利です。
- 整数を0で割ったり、0で剰余を求めたりすると実行時に例外が発生します。

なお、数値の符号を変える単項`-`や、値を1増減する`++`・`--`などもあります。まずは今回の5つの基本演算を使いこなせるようにしましょう。

<br><br>

## 参考資料

- [Java SE 17 言語仕様 - Multiplicative Operators（乗算・除算・剰余）](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.17)
- [Java SE 17 言語仕様 - Additive Operators（加算・減算）](https://docs.oracle.com/javase/specs/jls/se17/html/jls-15.html#jls-15.18)
- [Oracle Java Tutorials - Assignment, Arithmetic, and Unary Operators](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op1.html)（Java 8向けの教材です。この記事の基本演算はJava 17でも共通です）

