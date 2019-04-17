
# Polyfills

JavaScript言語は着実に進化しています。言語への新たな提案は定期的にだされ、それらは分析され、価値があると考えられたら <https://tc39.github.io/ecma262/> の一覧に追加され、[仕様](http://www.ecma-international.org/publications/standards/Ecma-262.htm) に進みます。

JavaScriptエンジンのチームは何を最初に実装するかについて独自の考えを持っています。彼らはドラフト段階の提案を実装する一方で、既に仕様となったものの実装を「面白くない、もしくはやるのが難しい」という理由で延期するかもしれません。

従って、あるエンジンに標準仕様の一部のみしか実装されていないという状況は非常に一般的なことです。

言語機能の現在のサポート状況を見るには <https://kangax.github.io/compat-table/es6/> が良いページです(それは大きく、まだ勉強すべき多くのことがあります)。

## Babel

我々が言語の最新の機能を使うとき、いくつかのエンジンはこのようなコードをサポートしていないかもしれません。先ほど言ったように、どこでもすべての機能が実装されている訳ではありません。

ここで、Babelが役に立ちます。

[Babel](https://babeljs.io) は [トランスパイラ](https://en.wikipedia.org/wiki/Source-to-source_compiler)です。
最新のJavaScriptコードを以前の標準仕様に書き直します。

実際には、Babelには２つのパートがあります:

<<<<<<< HEAD
1. １つ目はトランスパイラのプログラムで、コードを書き直します。開発者は自身のPC上でそれを実行します。するとコードが古い標準仕様のものに書き直されます。そして、コードはWebサイトにデリバリされます。[webpack](http://webpack.github.io/) や [brunch](http://brunch.io/) のような現代のプロジェクトのビルドシステムは、すべてのコード変更時に自動でトランスパイラを実行する手段を提供しています。そのため、私たち側で時間を取ることはありません。
=======
1. First, the transpiler program, which rewrites the code. The developer runs it on their own computer. It rewrites the code into the older standard. And then the code is delivered to the website for users. Modern project build system like [webpack](http://webpack.github.io/) or [brunch](http://brunch.io/) provide means to run transpiler automatically on every code change, so that doesn't involve any time loss from our side.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

2. ２つ目は polyfillです。

    トランスパイラはコードを書き直すので、構文機能はカバーされます。しかし、新しい関数のためには、それを実装する特別なスクリプトを書く必要があります。JavaScriptは非常に動的な言語であり、スクリプトは新しい機能を追加するだけでなく、組み込みの機能を変更することもできます。こうして、現代の標準に従って動作するようにすることができます。

    ギャップを "埋めて"、欠けている実装を加えるスクリプトとして、"poloyfill" という用語があります。

    興味深い２つの polyfill は:
    - [babel polyfill](https://babeljs.io/docs/usage/polyfill/) 多くをサポートしますが、大きいです.
    - [polyfill.io](http://polyfill.io) 必要な機能に応じて、オンデマンドで polyfill を読み込み/構築することができます。

従って、私たちはトランスパイラをセットアップし、古いエンジンが最新の機能をサポートするように polyfill を追加する必要があります。

もし、私たちが最新のエンジンを対象とし、どこでもサポートされているもの以外の機能を使わないのであれば、Babelを使う必要はありません。

## チュートリアルの例 


````online
ほとんどの例は次のように実行可能です:

```js run
alert('Press the "Play" button in the upper-right corner to run');
```

最新のJSを使った例は、あなたのブラウザがそれをサポートしている場合にだけ動作します。
````

```offline
オフライン版で呼んでいるのであれば、例は実行できませんが、通常動作します :)
```

[Chrome Canary](https://www.google.com/chrome/browser/canary.html) はすべての例に対して上手く動きます。他の最新のブラウザもほとんど大丈夫です。

本番では、Babelを使ってコードを最近のブラウザに適した形に変換できるので、このような制限はありません。コードはどこでも動くでしょう。
