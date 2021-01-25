# モダンなモード, "use strict"

<<<<<<< HEAD
長い間、JavaScriptは互換性の問題なしに進化していました。新しい機能は言語に追加されましたが、古い機能は変更されませんでした。

それは既存のコードが決して壊れないというメリットがありました。しかし、欠点はJavaScript作成者による間違いや不十分な決定がこの言語から抜け出せなくなったことです。

ECMAScript 5(ES5) が登場したときは2009年でした。新しい機能が言語に追加され、既存の機能のいくつかが修正されました。古いコードが動作するのを保つために、ほとんどの修正はデフォルトではOFFです。特別なディレクティブ `"use strict"` を明示的に有効にする必要があります。

[cut]
=======
For a long time, JavaScript evolved without compatibility issues. New features were added to the language while old functionality didn't change.

That had the benefit of never breaking existing code. But the downside was that any mistake or an imperfect decision made by JavaScript's creators got stuck in the language forever.

This was the case until 2009 when ECMAScript 5 (ES5) appeared. It added new features to the language and modified some of the existing ones. To keep the old code working, most such modifications are off by default. You need to explicitly enable them with a special directive: `"use strict"`.
>>>>>>> 97ef86242f9f236b13152e1baf52a55c4db8728a

## "use strict" 

<<<<<<< HEAD
そのディレクティブは文字列のように見えます: `"use strict"` もしくは `'use strict'`。 これがスクリプトの先頭に位置する場合、すべてのスクリプトは "最新の" 方法で動作します。

例えば
=======
The directive looks like a string: `"use strict"` or `'use strict'`. When it is located at the top of a script, the whole script works the "modern" way.

For example:
>>>>>>> 97ef86242f9f236b13152e1baf52a55c4db8728a

```js
"use strict";

// このコードはモダンな方法で動作します。
...
```

<<<<<<< HEAD
私たちはこの後 関数(コマンドをグループ化する方法) をすぐに学ぶでしょう。

先読みの備考として、`"use strict"` はスクリプト全体の代わりに関数(ほとんどの種類の関数) の頭に置くことができます。
その場合はその関数内でのみStrictモードが有効になります。しかし通常はスクリプト全体に対して使います。


````warn header="\"use strict\" が先頭にあることを保証してください"
`"use strict"` がスクリプトの先頭かを確認してください、そうでない場合 strict mode は有効でないかもしれません。

これは strict mode ではありません:

```js no-strict
alert("some code");
// 下の "use strict" は無視されます, 先頭にある必要があります
=======
Quite soon we're going to learn functions (a way to group commands), so let's note in advance that `"use strict"` can be put at the beginning of a function. Doing that enables strict mode in that function only. But usually people use it for the whole script.

````warn header="Ensure that \"use strict\" is at the top"
Please make sure that `"use strict"` is at the top of your scripts, otherwise strict mode may not be enabled.

Strict mode isn't enabled here:

```js no-strict
alert("some code");
// "use strict" below is ignored--it must be at the top
>>>>>>> 97ef86242f9f236b13152e1baf52a55c4db8728a

"use strict";

// strict mode はアクティブになりません
```

コメントだけは `"use strict"` の上に置けます。
````

<<<<<<< HEAD
```warn header="`use strict` をキャンセルする方法はありません"
`"no use strict"` または同系の古い振る舞いを返すようなディレクティブはありません。

一度 strict mode に入ったら戻ることはありません。
```

## 常に "use strict" 

`"use strict"` と "default" モードの違いはこの後にも説明があります。

次のチャプターでは、言語の機能を学びながら strict mode と default mode の違いについて説明します。幸い、それほど多くありません。そしてそれらは実際に我々の開発をより良くします。

現段階では、それについて一般的なことを知っていれば十分です:

1. `"use strict"` ディレクティブは "最新" モードにエンジンを切り替え、いくつかの組み込みの機能の振る舞いを変更します。勉強しながらその詳細を見ていきましょう。
2. strict mode は先頭の `"use strict"` で有効になります。また、自動的に strict mode を有効にする "classes" や "modules" のようないくつかの機能もあります。
3. strict mode はすべてのモダンブラウザによってサポートされています。
4. 常に `"use strict"` で始まるスクリプトは推奨されます。このチュートリアルのすべての例は、そうでないと明示されていない限り(ほとんどないですが)それを想定しています。
=======
```warn header="There's no way to cancel `use strict`"
There is no directive like `"no use strict"` that reverts the engine to old behavior.

Once we enter strict mode, there's no going back.
```

## Browser console

When you use a [developer console](info:devtools) to run code, please note that it doesn't `use strict` by default.

Sometimes, when `use strict` makes a difference, you'll get incorrect results.

So, how to actually `use strict` in the console?

First, you can try to press `key:Shift+Enter` to input multiple lines, and put `use strict` on top, like this:

```js
'use strict'; <Shift+Enter for a newline>
//  ...your code
<Enter to run>
```

It works in most browsers, namely Firefox and Chrome.

If it doesn't, e.g. in an old browser, there's an ugly, but reliable way to ensure `use strict`. Put it inside this kind of wrapper:

```js
(function() {
  'use strict';

  // ...your code here...
})()
```

## Should we "use strict"?

The question may sound obvious, but it's not so.

One could recommend to start scripts with `"use strict"`... But you know what's cool?

Modern JavaScript supports "classes" and "modules" - advanced language structures (we'll surely get to them), that enable `use strict` automatically. So we don't need to add the `"use strict"` directive, if we use them.

**So, for now `"use strict";` is a welcome guest at the top of your scripts. Later, when your code is all in classes and modules, you may omit it.**

As of now, we've got to know about `use strict` in general.

In the next chapters, as we learn language features, we'll see the differences between the strict and old modes. Luckily, there aren't many and they actually make our lives better.

All examples in this tutorial assume strict mode unless (very rarely) specified otherwise.
>>>>>>> 97ef86242f9f236b13152e1baf52a55c4db8728a
