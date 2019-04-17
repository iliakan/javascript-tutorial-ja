# データ型

<<<<<<< HEAD
JavaScriptの変数はどんなデータでも入れることができます。変数はある時点では文字列で、その後数値を受け取ることができます。:
=======
A variable in JavaScript can contain any data. A variable can at one moment be a string and at another be a number:
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

```js
// エラーなし
let message = "hello";
message = 123456;
```

このようなことができるプログラミング言語は "動的型付け" と呼ばれ、データ型はありますが、変数はそのどれにもバインドされないことを意味します。

<<<<<<< HEAD
JavaScriptでは7つの基本的なデータ型があります。ここでは基本を学び、次のチャプターでそれらの詳細について話しましょう。

[cut]
=======
There are seven basic data types in JavaScript. Here, we'll cover them in general and in the next chapters we'll talk about each of them in detail.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## 数値 

```js
let n = 123;
n = 12.345;
```

<<<<<<< HEAD
*数値* 型は整数と浮動小数点両方に使われます。

数値に関する多くの操作があります、 e.g. 乗算 `*`, 除算 `/`, 加算 `+`, 減算 `-` など。

通常の数値に加えて、これらのタイプに属する "特別な数値型" もあります。: `Infinity`、 `-Infinity`、 `NaN`.
=======
The *number* type represents both integer and floating point numbers.

There are many operations for numbers, e.g. multiplication `*`, division `/`, addition `+`, subtraction `-`, and so on.

Besides regular numbers, there are so-called "special numeric values" which also belong to this data type: `Infinity`, `-Infinity` and `NaN`.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

- `Infinity` は数学的な[無限大](https://en.wikipedia.org/wiki/Infinity) ∞ を表します。どの値よりも大きい特別な値です。

    ゼロによる除算でそれを得ることができます。:

    ```js run
    alert( 1 / 0 ); // 無限大
    ```

<<<<<<< HEAD
    もしくは、単にコードに直接書くこともできます:
=======
    Or just reference it directly:
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

    ```js run
    alert( Infinity ); // 無限大
    ```
- `NaN` は計算上のエラーを表します。正しくないもしくは未定義の数学的な操作の結果です。例:

    ```js run
    alert( "not a number" / 2 ); // NaN, このような除算は誤りです
    ```

<<<<<<< HEAD
    `NaN` は粘着性です。`NaN` 以降はどのような操作をしても `NaN` になります:
=======
    `NaN` is sticky. Any further operation on `NaN` returns `NaN`:
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

    ```js run
    alert( "not a number" / 2 + 5 ); // NaN
    ```

<<<<<<< HEAD
    そのため、数学的な表現の中のどこかに `NaN` がある場合、結果全体に伝搬します。

```smart header="算術演算子は安全です"
JavaScriptでは数学をするのは安全です。ゼロによる除算、数値ではない文字列を数値として扱う、など何でもできます。

スクリプトは致命的なエラー（"死"）で止まることはありません。 最悪の場合でも NaN という結果になります。
```

特別な数値は正式には "数値" 型に所属します。もちろん、常識では数値ではありませんが。
=======
    So, if there's a `NaN` somewhere in a mathematical expression, it propagates to the whole result.

```smart header="Mathematical operations are safe"
Doing maths is "safe" in JavaScript. We can do anything: divide by zero, treat non-numeric strings as numbers, etc.

The script will never stop with a fatal error ("die"). At worst, we'll get `NaN` as the result.
```

Special numeric values formally belong to the "number" type. Of course they are not numbers in the common sense of this word.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

チャプター <info:number> でより数値の動作について見ていきます。

## 文字列 

<<<<<<< HEAD
JavaScriptの文字列は引用符で囲む必要があります。
=======
A string in JavaScript must be surrounded by quotes.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

```js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed ${str}`;
```

JavScriptでは3種類の引用符があります。

1. ダブルクォート: `"Hello"`.
2. シングルクォート: `'Hello'`.
3. バッククォート: <code>&#96;Hello&#96;</code>.

ダブル/シングルクォートは "シンプルな" 引用符です。JavaScriptの中ではそれらに違いはありません。

バッククォートは "拡張機能" の引用符です。変数を `${…}` の中にラップすることで、変数を埋め込み文字列の中で表現することができます。たとえば:

```js run
let name = "John";

// 変数が埋め込まれた場合
alert( `Hello, *!*${name}*/!*!` ); // Hello, John!

// 式が埋め込まれた場合
alert( `the result is *!*${1 + 2}*/!*` ); // 結果は 3
```

<<<<<<< HEAD
`${…}` の中の表現は評価され、結果は文字列の一部になります。そこには何でも置くことができます: `name` のような変数、`1 + 2` のような算術表現、またはより複雑なものを書くこともできます。

これはバッククォートでのみ可能なことに留意してください。他のクォートはこのような埋め込みは許容しません!

=======
The expression inside `${…}` is evaluated and the result becomes a part of the string. We can put anything in there: a variable like `name` or an arithmetical expression like `1 + 2` or something more complex.

Please note that this can only be done in backticks. Other quotes don't have this embedding functionality!
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613
```js run
alert( "the result is ${1 + 2}" ); // 結果は ${1 + 2} です(ダブルクォートは何もしません)
```

チャプター<info:string> で、より深く文字列の説明をします。

```smart header="*character* 型はありません"
言語によっては、1文字のための特別な "文字" 型があります。たとえば、C言語やJavaでは、それは `char` です。

JavaScriptではこのような型はありません。`string` 型の1つなだけです。文字列は単一の文字または複数の文字から構成されます。
```

## boolean (論理型) 

boolean 型は2つの値だけを持ちます: `true` と `false`

この型は通常 yes/no の値を格納するために使われます: `true` は "yes" を意味し、 `false` は "no, 正しくない" を意味します。

例:

```js
let nameFieldChecked = true; // yes, 名前フィールドはチェックされている
let ageFieldChecked = false; // no, 年齢フィールドは未チェック
```

Boolean 値は比較の結果としても使われます:

```js run
let isGreater = 4 > 1;

alert( isGreater ); // true (比較結果は "yes" です)
```

<<<<<<< HEAD
後ほどチャプター<info:logical-operators>でbooleanのより詳細を説明します。
=======
We'll cover booleans more deeply in the chapter <info:logical-operators>.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## "null" 値 

<<<<<<< HEAD
特殊な `null` 値は上で述べたどの型にも属しません。

それは自身の別の型を形成し、`null` 値だけを含みます。
=======
The special `null` value does not belong to any of the types described above.

It forms a separate type of its own which contains only the `null` value:
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

```js
let age = null;
```

<<<<<<< HEAD
JavaScriptでは、 `null` は他の言語のような "存在しないオブジェクトへの参照" または "null へのポインタ" ではありません。

それは、 "無し"、"空" または "不明な値" と言った意味を持つ特別な値です。

上のコードは、 `age` は何らかの理由で不明な値もしくは空であることを述べています。
=======
In JavaScript, `null` is not a "reference to a non-existing object" or a "null pointer" like in some other languages.

It's just a special value which represents "nothing", "empty" or "value unknown".

The code above states that `age` is unknown or empty for some reason.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## "undefined" 値 

<<<<<<< HEAD
特殊な値 `undefined` も別に扱われます。`null` のように、それ自身の型を持ちます。
=======
The special value `undefined` also stands apart. It makes a type of its own, just like `null`.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

`undefined` の意味は "値は代入されていません" です。

<<<<<<< HEAD
もしも変数は宣言されているが代入されていない場合、その値は正確には `undefined` です:
=======
If a variable is declared, but not assigned, then its value is `undefined`:
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

```js run
let x;

alert(x); // "undefined" を表示
```

技術的にはどの変数にも `undefined` を代入することができます。

```js run
let x = 123;

x = undefined;

alert(x); // "undefined"
```

<<<<<<< HEAD
...しかし、そのようにするのは推奨されません。一般的には、 "空" や "不明な値" と言った用途では `null` を使い、`undefined` は変数が割り当てられているか、もしくは似たような確認のために使います。
=======
...But we don't recommend doing that. Normally, we use `null` to assign an "empty" or "unknown" value to a variable, and we use `undefined` for checks like seeing if a variable has been assigned.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## オブジェクトとシンボル 

`object` 型は特殊です。

<<<<<<< HEAD
他のすべての型は、値は1つのもの(文字列, 数値, または何でも)だけを含むので、"プリミティブ" と呼ばれます。対象的に、オブジェクトはデータのコレクションやより複雑なエンティティを格納するために使われます。ここでは、プリミティブについて十分に知った後、後ほどチャプター<info:object>で扱います。

`symbol` 型はオブジェクトの一意な識別子を作るのに使われます。完全性のためにここで言及していますが、オブジェクトの後で勉強するのがよいでしょう。
=======
All other types are called "primitive" because their values can contain only a single thing (be it a string or a number or whatever). In contrast, objects are used to store collections of data and more complex entities. We'll deal with them later in the chapter <info:object> after we learn more about primitives.

The `symbol` type is used to create unique identifiers for objects. We have to mention it here for completeness, but it's better to study this type after objects.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## typeof 操作 

<<<<<<< HEAD
`typeof` 操作は、引数の型を返します。異なる型の値を別々に処理したい、または素早くチェックしたいときに役立ちます。
=======
The `typeof` operator returns the type of the argument. It's useful when we want to process values of different types differently or just want to do a quick check.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

これは2つの形式の構文をサポートします:

<<<<<<< HEAD
1. 演算子として: `typeof x`.
2. 関数スタイル: `typeof(x)`.

言い換えると、それは括弧があってもなくても動作します。結果は同じです。
=======
1. As an operator: `typeof x`.
2. As a function: `typeof(x)`.

In other words, it works with parentheses or without them. The result is the same.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

`typeof x` の呼び出しは型名の文字列を返します。:

```js
typeof undefined // "undefined"

typeof 0 // "number"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

*!*
typeof Math // "object"  (1)
*/!*

*!*
typeof null // "object"  (2)
*/!*

*!*
typeof alert // "function"  (3)
*/!*
```

<<<<<<< HEAD
最後の3行については追加の説明が必要かもしれません:

1. `Math` は数学的な操作を提供する組み込みオブジェクトです。チャプター<info:number>で学ぶでしょう。ここでは、単にオブジェクトとしての例です。
2. `typeof null` の結果は `"object"` です。これは間違っています。これは `typeof` において、公式に認められているエラーで、互換性のために維持されています。もちろん、`null` はオブジェクトではありません。それは自身の別の型をもつ特殊な値です。なので、繰り返しますがそれは言語のエラーです。
3. `alert` は言語の機能なので、`typeof alert` の結果は `"function"` です。我々は次のチャプターで function を勉強します。そして、言語の中には特別な "function" 型がないことがわかるでしょう。function はオブジェクト型に属します。しかし `typeof` はそれらを別々に扱います。正式にはそれは正しくありませんが、実際にはとても便利です。
=======
The last three lines may need additional explanation:

1. `Math` is a built-in object that provides mathematical operations. We will learn it in the chapter <info:number>. Here, it serves just as an example of an object.
2. The result of `typeof null` is `"object"`. That's wrong. It is an officially recognized error in `typeof`, kept for compatibility. Of course, `null` is not an object. It is a special value with a separate type of its own. So, again, this is an error in the language.
3. The result of `typeof alert` is `"function"`, because `alert` is a function of the language. We'll study functions in the next chapters where we'll see that there's no special "function" type in JavaScript. Functions belong to the object type. But `typeof` treats them differently. Formally, it's incorrect, but very convenient in practice.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613


## サマリ 

JavaScriptには7つの基本型があります。

- `number` あらゆる種類の数値: 整数または浮動小数点
- `string` 文字列。文字列は1つかより多くの文字を持ち、別の1文字型はありません。
- `boolean` `true`/`false`
- `null` 不明な値 -- 単一の値 `null` を持つスタンドアロン型
- `undefined` 未割り当て値 -- 単一の値 `undefined` を持つスタンドアロン型
- `object` より複雑なデータ構造
- `symbol` 一意な識別子

<<<<<<< HEAD
`typeof` 操作は変数にどの型が格納されているかを知ることができます。

- 2つの形式: `typeof x` or `typeof(x)`.
- `"string"` のように型の名前の文字列を返します。
- `null` は `"object"` を返します -- それは言語のエラーで、実際はオブジェクトではありません。

次のチャプターではプリミティブ値について集中し、それらに精通した後オブジェクトに進みます。
=======
The `typeof` operator allows us to see which type is stored in a variable.

- Two forms: `typeof x` or `typeof(x)`.
- Returns a string with the name of the type, like `"string"`.
- For `null` returns `"object"` -- this is an error in the language, it's not actually an object.

In the next chapters, we'll concentrate on primitive values and once we're familiar with them, we'll move on to objects.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613
