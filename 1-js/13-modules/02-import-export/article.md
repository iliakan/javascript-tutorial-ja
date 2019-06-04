<<<<<<< HEAD

# エクスポートとインポート

エクスポート(export)とインポート(import)ディレクティブは非常に用途が広いです。

前のチャプターでは、シンプルな使用例を見ました。ここではより多くの例を見ていきましょう。

## 宣言の前の export

変数、関数、クラスのいずれかであれば、その前に `export` を置くことで、エクスポート対象として任意の宣言にラベル付けすることができます。

例えば、ここではすべてのエクスポートは有効です:

```js
// 配列のエクスポート
*!*export*/!* let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// 定数のエクスポート
*!*export*/!* const MODULES_BECAME_STANDARD_YEAR = 2015;

// クラスのエクスポート
=======
# Export and Import

Export and import directives are very versatile.

In the previous chapter we saw a simple use, now let's explore more examples.

## Export before declarations

We can label any declaration as exported by placing `export` before it, be it a variable, function or a class.

For instance, here all exports are valid:

```js
// export an array
*!*export*/!* let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// export a constant
*!*export*/!* const MODULES_BECAME_STANDARD_YEAR = 2015;

// export a class
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
*!*export*/!* class User {
  constructor(name) {
    this.name = name;
  }
}
```

<<<<<<< HEAD
````smart header="export class/function の後にセミコロンはありません"
クラスや関数の前の `export` はそれを [関数式](info:function-expressions-arrows) にはしないことに注意してください。エクスポートされていますが、依然として関数宣言です。

ほとんどの JavaScript のスタイルガイドは文のあとにセミコロンを推奨しますが、関数とクラス宣言の後は推奨しません。

そういうわけで、`export class` と `export function` の末尾にはセミコロンがありません。
=======
````smart header="No semicolons after export class/function"
Please note that `export` before a class or a function does not make it a [function expression](info:function-expressions-arrows). It's still a function declaration, albeit exported.

Most JavaScript style guides recommend semicolons after statements, but not after function and class declarations.

That's why there should be no semicolons at the end of `export class` and `export function`.
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
export function sayHi(user) {
  alert(`Hello, ${user}!`);
<<<<<<< HEAD
} *!* // 末尾に ; はありません */!*
=======
} *!* // no ; at the end */!*
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
```

````

<<<<<<< HEAD
## 宣言とは別に export する

また、別に `export` を置くこともできます。

ここでは、最初に宣言をし、その後エクスポートしています:
=======
## Export apart from declarations

Also, we can put `export` separately.

Here we first declare, and then export:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js  
// 📁 say.js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

*!*
<<<<<<< HEAD
export {sayHi, sayBye}; // エクスポートされた変数のリスト
*/!*
```

...あるいは、技術的には関数の上に `export` を置くこともできます。

## import *

通常は、次のようにインポートするものの一覧を `import {...}` に置きます。:
=======
export {sayHi, sayBye}; // a list of exported variables
*/!*
```

...Or, technically we could put `export` above functions as well.

## Import *

Usually, we put a list of what to import into `import {...}`, like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
*!*
import {sayHi, sayBye} from './say.js';
*/!*

sayHi('John'); // Hello, John!
sayBye('John'); // Bye, John!
```

<<<<<<< HEAD
しかし、リストが長い場合、`import * as <obj>` を使用してオブジェクトとしてすべてをインポートすることができます。例:
=======
But if the list is long, we can import everything as an object using `import * as <obj>`, for instance:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
*!*
import * as say from './say.js';
*/!*

say.sayHi('John');
say.sayBye('John');
```

<<<<<<< HEAD
一見すると、"import everything" は非常にクールに思えます。が、そもそも、なぜインポートが必要なものを明示的にリストすると必要があるのでしょう？

それにはいくつかの理由があります。

1. 現代のビルドツール ([webpack](http://webpack.github.io) など) はモジュールをまとめ、読み込みを高速化するために最適化を行ったり、未使用なものを削除します。

    我々のプロジェクトに多くの機能を持つサードパーティのライブラリ `lib.js` を追加したとしましょう。:
=======
At first sight, "import everything" seems such a cool thing, short to write, why should we ever explicitly list what we need to import?

Well, there are few reasons.

1. Modern build tools ([webpack](http://webpack.github.io) and others) bundle modules together and optimize them to speedup loading and remove unused stuff.

    Let's say, we added a 3rd-party library `lib.js` to our project with many functions:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
    ```js
    // 📁 lib.js
    export function sayHi() { ... }
    export function sayBye() { ... }
    export function becomeSilent() { ... }
    ```

<<<<<<< HEAD
    いま、我々のプロジェクトで実際に必要なのはそのうちの1つだけです。
=======
    Now if we only use one of `lib.js` functions in our project:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
    ```js
    // 📁 main.js
    import {sayHi} from './lib.js';
    ```
<<<<<<< HEAD
    ...その後、最適化処理は自動的にそれを検知し、バンドルされているコードから他の機能を完全に除去します。したがって、微づ路は小さくなります。それは "tree-shaking" と呼ばれています。

2. 何をインポートするかを明示的にリストすることは、より短い名前を与えます: `lib.sayHi()` の代わりに `sayHi()`
3. 明示的なインポートはコード構造の見通しをよりよくします。: 何がどこで使われているか。それはコードをサポートし、リファクタリングをより簡単にします。

## import "as"

異なる名前でインポートするために `as` を使うこともできます。

例えば、簡潔にするために `sayHi` をローカル変数 `hi` にインポートしましょう。`sayBye` も同様です。:
=======
    ...Then the optimizer will automatically detect it and totally remove the other functions from the bundled code, thus making the build smaller. That is called "tree-shaking".

2. Explicitly listing what to import gives shorter names: `sayHi()` instead of `lib.sayHi()`.
3. Explicit imports give better overview of the code structure: what is used and where. It makes code support and refactoring easier.

## Import "as"

We can also use `as` to import under different names.

For instance, let's import `sayHi` into the local variable `hi` for brevity, and same for `sayBye`:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
*!*
import {sayHi as hi, sayBye as bye} from './say.js';
*/!*

hi('John'); // Hello, John!
bye('John'); // Bye, John!
```

## Export "as"

<<<<<<< HEAD
同様の構文は `export` にも存在します。

関数を `hi` と `bye` としてエクスポートしましょう。:
=======
The similar syntax exists for `export`.

Let's export functions as `hi` and `bye`:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 say.js
...
export {sayHi as hi, sayBye as bye};
```

<<<<<<< HEAD
今、`hi` と `bye` は外部にとって公式な名前になります。:
=======
Now `hi` and `bye` are official names for outsiders:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
import * as say from './say.js';

say.hi('John'); // Hello, John!
say.bye('John'); // Bye, John!
```

## export default

<<<<<<< HEAD
これまでのところ、複数のものをインポート/エクスポートする方法を見てきました(必要に応じて "as" で別名で扱います)。

実際には、モジュールは次のいずれかを含んでいます:
- ライブラリ、`lib.js` のような多く関数の集まり
- あるいは、`class User` のようなエンティティが `user.js` に記述されている場合。モジュール全体はこのクラスのみを持ちます。

ほとんどの場合、2番めのアプローチが好まれます。

当然のことながら、モジュールシステムでは、すべてが独自のモジュールになるため、多くのファイルが必要となります。が、それはまったく問題ではありません。実際には、ファイルが良く名前付けされ、フォルダに構造化されていれば、コードのナビゲーションはとても簡単になります。

合わせて、モジュールは、特別な `export default` 構文を提供し、"モジュール毎に1つのもの" のように見栄えを良くします。

これは以下の `export` と `import` 文を必要とします。:

1. モジュールの "メインのエクスポート" の前に `export default` を置きます。
2. 括弧なしで `import` を呼び出します。

例えば、`user.js` は `class User` をエクスポートします:

```js
// 📁 user.js
export *!*default*/!* class User { // "default" を追加するだけ
=======
So far, we've seen how to import/export multiple things, optionally "as" other names.

In practice, modules contain either:
- A library, pack of functions, like `lib.js`.
- Or an entity, like `class User` is described in `user.js`, the whole module has only this class.

Mostly, the second approach is preferred, so that every "thing" resides in its own module.

Naturally, that requires a lot of files, as everything wants its own module, but that's not a problem at all. Actually, code navigation becomes easier, if files are well-named and structured into folders.

Modules provide special `export default` syntax to make "one thing per module" way look better.

It requires following `export` and `import` statements:

1. Put `export default` before the "main export" of the module.
2. Call `import` without curly braces.

For instance, here `user.js` exports `class User`:

```js
// 📁 user.js
export *!*default*/!* class User { // just add "default"
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
  constructor(name) {
    this.name = name;
  }
}
```

<<<<<<< HEAD
...そして `main.js` はそれをインポートします:

```js
// 📁 main.js
import *!*User*/!* from './user.js'; // {User} ではなく User
=======
...And `main.js` imports it:

```js
// 📁 main.js
import *!*User*/!* from './user.js'; // not {User}, just User
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

new User('John');
```

<<<<<<< HEAD
波括弧なしのインポートは見栄えがよくなります。モジュールを使い始めるときによくある間違いは、波括弧を忘れてしまうことです。なので、覚えておいてください。`import` は名前付けインポートの場合には波括弧が必要であり、デフォルトインポートの場合には不要です。

| 名前付きエクスポート | デフォルトエクスポート |
=======
Imports without curly braces look nicer. A common mistake when starting to use modules is to forget curly braces at all. So, remember, `import` needs curly braces for named imports and doesn't need them for the default one.

| Named export | Default export |
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
|--------------|----------------|
| `export class User {...}` | `export default class User {...}` |
| `import {User} from ...` | `import User from ...`|

<<<<<<< HEAD
もちろん、1つのファイルには、1つしか "default" エクスポートはありません。

1つのモジュールの中で、デフォルトと名前付きエクスポート両方をもたせることもできますが、実際には、通常は混在させません。モジュールは名前付きエクスポート、あるいはデフォルトいずれかを持ちます。

**もう1点注意すべきことは、名前付きエクスポートは名前を持たなければならない(当然ですが)のに対し、`export default` は匿名の場合があります。**

例えば、これらはすべて有効なデフォルトエクスポートです:

```js
export default class { // クラス名なし
  constructor() { ... }
}

export default function(user) { // 関数名なし
  alert(`Hello, ${user}!`);
}

// 変数の作成なしで単一値のエクスポート
export default ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
```

これは問題ありません。なぜなら `export default` はファイル毎に1つのみだけだからです。そのため、`import` は何をインポートすべきか常に知っています。
一方、名前付きエクスポートの名前を省略するとエラーになります。:

```js
export class { // Error! (非デフォルトエクスポートは名前が必要です)
=======
Naturally, there may be only one "default" export per file.

We may have both default and named exports in a single module, but in practice people usually don't mix them. A module has either named exports or the default one.

**Another thing to note is that named exports must (naturally) have a name, while `export default` may be anonymous.**

For instance, these are all perfectly valid default exports:

```js
export default class { // no class name
  constructor() { ... }
}

export default function(user) { // no function name
  alert(`Hello, ${user}!`);
}

// export a single value, without making a variable
export default ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
```

That's fine, because `export default` is only one per file. Contrary to that, omitting a name for named imports would be an error:

```js
export class { // Error! (non-default export needs a name)
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
  constructor() {}
}
```     

<<<<<<< HEAD
### "default" エイリアス

"default" という単語は、デフォルトエクスポートのための "エイリアス" の1つです。

例えば、すでに関数が宣言されている場合、それを `export default` する方法は次の通りです:
=======
### "Default" alias

The "default" keyword is used as an "alias" for the default export, for standalone exports and other scenarios when we need to reference it.

For example, if we already have a function declared, that's how to `export default` it (separately from the definition):
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

<<<<<<< HEAD
export {sayHi as default}; // 関数の前に "export default" を追加する場合と同じです
```

あるいは、モジュール `user.js` が1つのメインの "デフォルト" のものと、いくつかの名前付きのものをエクスポートする場合(めったにありませんが起こりえます)、次のようになります:
=======
export {sayHi as default}; // same as if we added "export default" before the function
```

Or, let's say a module `user.js` exports one main "default" thing and a few named ones (rarely the case, but happens):
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 user.js
export default class User {
  constructor(name) {
    this.name = name;
  }
}

export function sayHi(user) {
  alert(`Hello, ${user}!`);
}
```

<<<<<<< HEAD
名前付きと一緒にデフォルトエクスポートをインポートする方法です:
=======
Here's how to import the default export along with a named one:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
import {*!*default as User*/!*, sayHi} from './user.js';

new User('John');
```

<<<<<<< HEAD
あるいは、オブジェクトとして `*` をインポートする場合、`default` プロパティはまさにデフォルトエクスポートです:
=======
Or, if we consider importing `*` as an object, then the `default` property is exactly the default export:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 main.js
import * as user from './user.js';

let User = user.default;
new User('John');
```


<<<<<<< HEAD
### デフォルトエクスポートを使うべきですか？

デフォルトエクスポートを使用する際は注意が必要です。なぜなら、それらはメンテナンスがいくらか異なるためです。

名前付きエクスポートは明示的です。それらは正確にインポートするものを命名するので、そこから情報を得ることができます。これは良いことです。

また、名前付きエクスポートは、インポートするのに正確に正しい名前を使うことを強制します。

```js
import {User} from './user.js';
```

デフォルトエクスポートの場合、独自の名前を作成する必要があります。:

```js
import MyUser from './user.js'; // なにかをインポートします
```

したがって、チームメンバは同じものに異なる名前を使用することができてしまうため、そこには誤用される余地があります。

通常、それを避け、コードの一貫性を保つため、インポートされた変数はファイル名に対応するべきであるという規則があります。例えば:
=======
### Should I use default exports?

One should be careful about using default exports, because they are more difficult to maintain.

Named exports are explicit. They exactly name what they import, so we have that information from them, that's a good thing.

Also, named exports enforce us to use exactly the right name to import:

```js
import {User} from './user.js';
// import {MyUser} won't work, the name must be {User}
```

For default exports, we always choose the name when importing:

```js
import User from './user.js'; // works
import MyUser from './user.js'; // works too
// could be import Anything..., and it'll be work
```

So, there's a little bit more freedom that can be abused, so that team members may use different names for the same thing.

Usually, to avoid that and keep the code consistent, there's a rule that imported variables should correspond to file names, e.g:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
import User from './user.js';
import LoginForm from './loginForm.js';
import func from '/path/to/func.js';
...
```

<<<<<<< HEAD
別の解決策は、どこでも名前付きエクスポートを使用することです。たとえ単一のものだけがエクスポートされるとしても、`default` なしで名前付きでエクスポートします。

これは、再エクスポート(後述)を少しだけ簡単にもします。

## 再エクスポート

"再エクスポート" 構文 `export ... from ...` を使うと、インポートをした直後にそれらを(場合により別の名前で)エクスポートすることができます。
=======
Another solution would be to use named exports everywhere. Even if only a single thing is exported, it's still exported under a name, without `default`.

That also makes re-export (see below) a little bit easier.

## Re-export

"Re-export" syntax `export ... from ...` allows to import things and immediately export them (possibly under another name), like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
export {sayHi} from './say.js';
export {default as User} from './user.js';
```

<<<<<<< HEAD
要点は何で、なぜこれが必要なのでしょう？実用的なユースケースを見てみましょう。

"パッケージ" を書いていると想像してください。: 多くのモジュールを持ち、主に内部で必要とされ、いくつかの機能を外部にエクスポートされたフォルダ(NPMのようなツールはパッケージの公開と配布を可能にしますが、ここではそれは関係ありません。)

ディレクトリ構造は次のようになります:
=======
What's the point, why that's needed? Let's see a practical use case.

Imagine, we're writing a "package": a folder with a lot of modules, mostly needed internally, with some of the functionality exported outside (tools like NPM allow to publish and distribute packages, but here it doesn't matter).

A directory structure could be like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
```
auth/
  index.js  
  user.js
  helpers.js
  tests/
    login.js
  providers/
    github.js
    facebook.js
    ...
```

<<<<<<< HEAD
単一のエントリポイントである "メインファイル" の `auth/index.js` を通してパッケージの機能を公開したいです。次にように:
=======
We'd like to expose the package functionality via a single entry point, the "main file" `auth/index.js`, to be used like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
import {login, logout} from 'auth/index.js'
```

<<<<<<< HEAD
この考えは、部外者(我々のパッケージを使う開発者)は、その内部構造に干渉する必要はないということです。彼らは我々のパッケージフォルダの中のファイルを検索するべきではありません。我々は `auth/index.js` に必要なものだけをエクスポートし、残りの部分は詮索好きな目から隠れたままにします。

いま、実際にエクスポートされた機能はパッケージ内に散らかっているので、それらを集めて `auth/index.js` で "再エクスポート" します。:
=======
The idea is that outsiders, developers who use our package, should not meddle with its internal structure. They should not search for files inside our package folder. We export only what's necessary in `auth/index.js` and keep the rest hidden from prying eyes.

Now, as the actual exported functionality is scattered among the package, we can gather and "re-export" it in `auth/index.js`:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 auth/index.js
import {login, logout} from './helpers.js';
export {login, logout};

import User from './user.js';
export {User};

<<<<<<< HEAD
import Githib from './providers/github.js';
=======
import Github from './providers/github.js';
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
export {Github};
...
```

<<<<<<< HEAD
"再エクスポート" はそれの短縮記法です:
=======
"Re-exporting" is just a shorter notation for that:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
// 📁 auth/index.js
export {login, logout} from './helpers.js';
<<<<<<< HEAD
// あるいは、すべてのヘルパーを再エクスポートするには、次のようにします:
=======
// or, to re-export all helpers, we could use:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
// export * from './helpers.js';

export {default as User} from './user.js';

<<<<<<< HEAD
export {default as Githib} from './providers/github.js';
...
```

````warn header="デフォルトの再エクスポートは用心が必要です"
注意: `export User from './user.js'` は動作しません。実際には構文エラーです。デフォルトエクスポートを再エクスポートするには、明示的に `{default as ...}` と言及しなければなりません。上の例のように。

また、もう1つ奇妙なことがあります。: `export * from './user.js'` は名前付けエクスポートのみを再エクスポートし、デフォルトは含まれていません。改めて言いますが、明示的に言及する必要があります。

例えば、すべてを再エクスポートするには、2つの文が必要になります。:

=======
export {default as Github} from './providers/github.js';
...
```

````warn header="Re-exporting default is tricky"
Please note: `export User from './user.js'` won't work. It's actually a syntax error. To re-export the default export, we must mention it explicitly `{default as ...}`, like in the example above.

Also, there's another oddity: `export * from './user.js'` re-exports only named exports, excluding the default one. Once again, we need to mention it explicitly.

For instance, to re-export everything, two statements will be necessary:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
```js
export * from './module.js'; // to re-export named exports
export {default} from './module.js'; // to re-export default
```

<<<<<<< HEAD
デフォルトは再エクスポートするときのみ明示的な言及が必要です。: `import * as obj` は動作します。これは `obj.default` としてデフォルトエクスポートをインポートします。なので、インポートとエクスポートの間には少し非対称性があります。
````

## サマリ

`export` には以下の種類があります:

- 宣言の前:
  - `export [default] class/function/variable ...`
- スタンドアロン:
  - `export {x [as y], ...}`.
- 再エクスポート:
  - `export {x [as y], ...} from "mod"`
  - `export * from "mod"` (デフォルトは再エクスポートしない).
  - `export {default [as y]} from "mod"` (デフォルトの再エクスポート).

Import:

- モジュールから名前付きエクスポート:
  - `import {x [as y], ...} from "mod"`
- デフォルトエクスポート:  
  - `import x from "mod"`
  - `import {default as x} from "mod"`
- すべて:
  - `import * as obj from "mod"`
- モジュールの取得/評価のみでインポートはしない:
  - `import "mod"`

import/export 文を他のコードの前後に置くことができ、どちらでも同じ結果になります。

なので、これも技術的には問題ありません:
```js
sayHi();

import {sayHi} from './say.js'; // ファイルの末尾で import
```

実際には、インポートは通常ファイルの先頭にありますが、それは利便性のためだけです。

**import/export 文は `{...}` の中では動作しないことに注意してください**

このような条件付きのインポートは動作しません:
=======
The default should be mentioned explicitly only when re-exporting: `import * as obj` works fine. It imports the default export as `obj.default`. So there's a slight asymmetry between import and export constructs here.
````

## Summary

There are following types of `export`:

- Before declaration:
  - `export [default] class/function/variable ...`
- Standalone:
  - `export {x [as y], ...}`.
- Re-export:
  - `export {x [as y], ...} from "mod"`
  - `export * from "mod"` (doesn't re-export default).
  - `export {default [as y]} from "mod"` (re-export default).

Import:

- Named exports from module:
  - `import {x [as y], ...} from "mod"`
- Default export:  
  - `import x from "mod"`
  - `import {default as x} from "mod"`
- Everything:
  - `import * as obj from "mod"`
- Import the module (it runs), but do not assign it to a variable:
  - `import "mod"`

We can put import/export statements at the top or at the bottom of a script, that doesn't matter.

So this is technically fine:
```js
sayHi();

// ...

import {sayHi} from './say.js'; // import at the end of the script
```

In practice imports are usually at the start of the file, but that's only for better convenience.

**Please note that import/export statements don't work if inside `{...}`.**

A conditional import, like this, won't work:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
```js
if (something) {
  import {sayHi} from "./say.js"; // Error: import must be at top level
}
```

<<<<<<< HEAD
...しかし仮に本当に条件に応じてなにかをインポートする必要がある場合はどうなるでしょう？あるいは、本当に必要なときに要求に応じてモジュールをロードするような場合です。

次のチャプターではダイナミックインポートを見ていきます。
=======
...But what if we really need to import something conditionally? Or at the right time? Like, load a module upon request, when it's really needed?

We'll see dynamic imports in the next chapter.
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
