
# Fetch API

<<<<<<< HEAD
これまでの記事で、私たちは fetch について多くのことを知っています。

それでは、そのすべての機能をカバーするために、API の残りの部分を見ていきましょう。

以下は、指定可能なすべての fetch オプションとそのデフォルト値(コメントは他の選択肢です)のリストです。:
=======
So far, we know quite a bit about fetch.

Now let's see the rest of API, to cover all its abilities.

Here's the full list of all possible fetch options with their default values (alternatives in comments):
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
let promise = fetch(url, {
  method: "GET", // POST, PUT, DELETE, etc.
  headers: {
<<<<<<< HEAD
    "Content-Type": "text/plain;charset=UTF-8" // 文字列の本文の場合, 本文に依存します
  },
  body: undefined // 文字列, FormData, Blob, BufferSource, あるいは URLSearchParams
  referrer: "about:client", // no-referrer の場合は "", あるいは現在のオリジンの URL
=======
    "Content-Type": "text/plain;charset=UTF-8" // for a string body, depends on body
  },
  body: undefined // string, FormData, Blob, BufferSource, or URLSearchParams
  referrer: "about:client", // "" for no-referrer, or an url from the current origin
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
  referrerPolicy: "no-referrer-when-downgrade", // no-referrer, origin, same-origin...
  mode: "cors", // same-origin, no-cors
  credentials: "same-origin", // omit, include
  cache: "default", // no-store, reload, no-cache, force-cache, or only-if-cached
  redirect: "follow", // manual, error
<<<<<<< HEAD
  integrity: "", // "sha256-abcdef1234567890" のようなハッシュ
  keepalive: false, // true
  signal: undefined, // リクスとを中止するための AbortController
=======
  integrity: "", // a hash, like "sha256-abcdef1234567890"
  keepalive: false, // true
  signal: undefined, // AbortController to abort request
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
  window: window // null
});
```

<<<<<<< HEAD
チャプター <info:fetch-basics> で `method`, `headers` そして `body` を詳しく説明しました。

`signal` オプションは <info:fetch-abort> で説明しています。

それでは、オプションの残りを調べてみましょう。

## referrer, referrerPolicy

これらのオプションは `fetch` がどのように HTTP `Referer` へヘッダを設定するかを管理します。

そのヘッダには、リクエストを行ったページの URL が含まれます。ほとんどの場合、これは非常に小さな情報の役割を果たしますが、セキュリティ目的で削除または変更するのが理にかなっていることがあります。

**`referrer` オプションにより、現在のオリジン内の任意の `Referer` を設定するか、それを無効にすることができます。**

referer を送らないようにするには、空文字をセットします:
```js
fetch('/page', {
*!*
  referrer: "" // Referer ヘッダなし
=======
An impressive list, right?

We fully covered `method`, `headers` and `body` in the chapter <info:fetch-basics>.

The `signal` option is covered in <info:fetch-abort>.

Now let's explore the rest of options.

## referrer, referrerPolicy

These options govern how `fetch` sets HTTP `Referer` header.

That header contains the url of the page that made the request. In most scenarios, it plays a very minor informational role, but sometimes, for security purposes, it makes sense to remove or modify it.
.

**The `referrer` option allows to set any `Referer` within the current origin) or disable it.**

To send no referer, set an empty string:
```js
fetch('/page', {
*!*
  referrer: "" // no Referer header
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
*/!*
});
```

<<<<<<< HEAD
現在のオリジン内の別の URL を設定するには次のようにします:

```js
fetch('/page', {
  // https://javascript.info にいる想定です
  // 任意の Referer ヘッダが設定できますが、現在のオリジン内のみです
=======
To set another url within the current origin:

```js
fetch('/page', {
  // assuming we're on https://javascript.info
  // we can set any Referer header, but only within the current origin
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
*!*
  referrer: "https://javascript.info/anotherpage"
*/!*
});
```

<<<<<<< HEAD
**`referrerPolicy` オプションは `Referer` に対する一般的なルールを設定します。**

指定可能な値は[Referrer Policy specification](https://w3c.github.io/webappsec-referrer-policy/)で説明されています:

- **`"no-referrer-when-downgrade"`** -- デフォルト値: HTTPS から HTTP (より安全性の低いプロトコル)にリクエストを送信する場合以外は、常に `Referer` は送信されます。
- **`"no-referrer"`** -- けして `Referer` を送信しません。
- **`"origin"`** -- `Referer` には完全なページURLではなく、オリジンのみを送信します。例えば、`http://site.com/path` の代わりに `http://site.com`。
- **`"origin-when-cross-origin"`** -- 同じオリジンには完全な referrer を送信しますが、クロスオリジンリクエストの場合はオリジン部分のみを送信します。
- **`"same-origin"`** -- 同じオリジンには完全な referrer を送信しますが、クロスオリジンリクエストの場合は referrer を送信しません。
- **`"strict-origin"`** -- オリジンのみを送信し、HTTPS→HTTP のリクエストの場合には referrer を送信しません。
- **`"strict-origin-when-cross-origin"`** -- 同じオリジンの場合は完全な referrer を送信し、クロスオリジンの場合はHTTPS→HTTP リクエストでなければオリジンのみを送信、 HTTPS→HTTP の場合は何も送信しません。

外部からは見えるべきでないURL構造をもつ管理者の区域があるとします。

もしクロスオリジンの `fetch` を送信した場合、デフォルトでは自身のページの完全なURLを持つ `Referer` ヘッダを送信します(HTTPS から HTTP へリクエストする場合を除く。この場合は `Referer` はありません)。

E.g. `Referer: https://javascript.info/admin/secret/paths`.

referrer を完全に隠したい場合:

```js
fetch('https://another.com/page', {
  referrerPolicy: "no-referrer" // Referer なし。 referrer: "" と同じです。
});
```

そうではなく、リモート側でリクエストがどこから来たのかを確認したい場合には、URLの "オリジン" 部分だけを送ることができます。:
=======
**The `referrerPolicy` option sets general rules for `Referer`.**

Possible values are described in the [Referrer Policy specification](https://w3c.github.io/webappsec-referrer-policy/):

- **`"no-referrer-when-downgrade"`** -- default value: `Referer` is sent always, unless we send a request from HTTPS to HTTP (to less secure protocol).
- **`"no-referrer"`** -- never send `Referer`.
- **`"origin"`** -- only send the origin in `Referer`, not the full page URL, e.g. `http://site.com` instead of `http://site.com/path`.
- **`"origin-when-cross-origin"`** -- send full referrer to the same origin, but only the origin part for cross-origin requests.
- **`"same-origin"`** -- send full referrer to the same origin, but no referer for for cross-origin requests.
- **`"strict-origin"`** -- send only origin, don't send referrer for HTTPS→HTTP requests.
- **`"strict-origin-when-cross-origin"`** -- for same-origin send full referrer, for cross-origin send only origin, unless it's HTTPS→HTTP request, then send nothing.
- **`"unsafe-url"`** -- always send full url in `Referer`.

Let's say we have an admin zone with URL structure that shouldn't be visible from outside.

If we send a cross-origin `fetch`, then by default it sends the `Referer` header with the full url of our page (except when we request from HTTPS to HTTP, then no `Referer`).

E.g. `Referer: https://javascript.info/admin/secret/paths`.

If we'd like to totally hide the referrer:

```js
fetch('https://another.com/page', {
  referrerPolicy: "no-referrer" // no Referer, same effect as referrer: ""
});
```

Otherwise, if we'd like the remote side to see where the request comes from, we can send only the "origin" part of the url:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
fetch('https://another.com/page', {
  referrerPolicy: "strict-origin" // Referer: https://javascript.info
});
```

## mode

<<<<<<< HEAD
`mode` オプションはクロスオリジンリクエストを防ぐ安全装置として機能します。:

- **`"cors"`** -- デフォルト。<info:fetch-crossorigin> で説明されているように、クロスオリジンリクエストは許可されます。,
- **`"same-origin"`** -- クロスオリジンリクエストは禁止されています,
- **`"no-cors"`** -- 単純なクロスオリジンリクエストのみ許可されています。

これは、fetch URL がサードパーティから来たもので、クロスオリジンの機能を制限するために "機能をオフ" にしたい場合に役立ちます。

## credentials

`credentials` オプションは、`fetch` がリクエストと一緒に cookie と HTTP-Authorization ヘッダを送るべきかを指定するものです。

- **`"same-origin"`** -- デフォルトです。クロスオリジンリクエストに対しては送信しません。
- **`"include"`** -- 常に送信し、クロスオリジンのサーバから  `Accept-Control-Allow-Credentials` を要求します,
- **`"omit"`** -- 同一オリジンのリクエストの場合でも送信しません。

## cache

デフォルトでは、`fetch` リクエストは標準の HTTP キャッシングを使用します。つまり、`Expires` や `Cache-Control` ヘッダに従ったり、`If-Modified-Since` を送信したりします。通常のHTTPリクエストがするのと同じようにします。

`cache` オプションを使うことで、HTTP キャッシュを無視あるいはその使い方を調整することができます。:

- **`"default"`** --  `fetch` は標準の HTTP キャッシュのルールとヘッダを使用します;
- **`"no-store"`** -- HTTP キャッシュを完全に無視します。 `If-Modified-Since`, `If-None-Match`, `If-Unmodified-Since`, `If-Match`, または `If-Range` のヘッダを設定している場合は、このモードがデフォルトになります;
- **`"reload"`** -- (たとえキャッシュされていたとしても)HTTP キャッシュから結果を取りませんが、キャッシュにレスポンスを埋めます(レスポンスヘッダが許可している場合)。
- **`"no-cache"`** -- キャッシュされているレスポンスがある場合は条件付きリクエストを作成し、それ以外の場合は通常のリクエストを作成します。レスポンスで HTTP キャッシュを埋めます。
- **`"force-cache"`** -- たとえ古くてもHTTP キャッシュからのレスポンスを使用します。HTTPキャッシュにレスポンスがない場合は、通常の HTTP リクエストを行い通常通りの振る舞いをします;
- **`"only-if-cached"`** -- たとえ古くてもHTTP キャッシュからのレスポンスを使用します。HTTPキャッシュにレスポンスがない場合、エラーになります。 `mode` が `"same-origin"` の場合にのみ動作します。

## redirect

通常、 `fetch` は 301 や 302 などのように、HTTP リダイレクトに透過的に従います。

`redirect` オプションでそれを変更することができます:

- **`"follow"`** -- デフォルト。HTTP リダイレクトに従います,
- **`"error"`** -- HTTP リダイレクトの場合にはエラーになります。,
- **`"manual"`** -- HTTP リダイレクトには従いませんが、`response.url` が新しい URL になり、`response.redirected` が `true` になります。必要に応じて新しい URL へ手動でリダイレクトすることができます。

## integrity

`integrity` オプションは、レスポンスが既知のチェックサムに一致するかを確認することができます。

[仕様](https://w3c.github.io/webappsec-subresource-integrity/) で説明されている通り、サポートされているハッシュ関数は SHA-256, SHA-384, と SHA-512 であり、ブラウザによっては他のものがあるかもしれません。

例えば、ファイルをダウンロードし、その SHA-256 のチェックサムが "abc" とします（実際のチェックサムはもちろんもっと長いです）。

これを次のようにして、`integrity` オプションに指定することができます:
=======
The `mode` option serves as a safe-guard that prevents cross-origin requests:

- **`"cors"`** -- the default, cross-origin requests are allowed, as described in <info:fetch-crossorigin>,
- **`"same-origin"`** -- cross-origin requests are forbidden,
- **`"no-cors"`** -- only simple cross-origin requests are allowed.

That may be useful in contexts when the fetch url comes from 3rd-party, and we want a "power off switch" to limit cross-origin capabilities.

## credentials

The `credentials` option specifies whether `fetch` should send cookies and HTTP-Authorization headers with the request.

- **`"same-origin"`** -- the default, don't send for cross-origin requests,
- **`"include"`** -- always send, requires `Accept-Control-Allow-Credentials` from cross-origin server,
- **`"omit"`** -- never send, even for same-origin requests.

## cache

By default, `fetch` requests make use of standard HTTP-caching. That is, it honors `Expires`, `Cache-Control` headers, sends `If-Modified-Since`, and so on. Just like regular HTTP-requests do.

The `cache` options allows to ignore HTTP-cache or fine-tune its usage:

- **`"default"`** -- `fetch` uses standard HTTP-cache rules and headers;
- **`"no-store"`** -- totally ignore HTTP-cache, this mode becomes the default if we set a header `If-Modified-Since`, `If-None-Match`, `If-Unmodified-Since`, `If-Match`, or `If-Range`;
- **`"reload"`** -- don't take the result from HTTP-cache (if any), but populate cache with the response (if response headers allow);
- **`"no-cache"`** -- create a conditional request if there is a cached response, and a normal request otherwise. Populate HTTP-cache with the response;
- **`"force-cache"`** -- use a response from HTTP-cache, even if it's stale. If there's no response in HTTP-cache, make a regular HTTP-request, behave normally;
- **`"only-if-cached"`** -- use a response from HTTP-cache, even if it's stale. If there's no response in HTTP-cache, then error. Only works when `mode` is `"same-origin"`.

## redirect

Normally, `fetch` transparently follows HTTP-redirects, like 301, 302 etc.

The `redirect` option allows to change that:

- **`"follow"`** -- the default, follow HTTP-redirects,
- **`"error"`** -- error in case of HTTP-redirect,
- **`"manual"`** -- don't follow HTTP-redirect, but `response.url` will be the new URL, and `response.redirected` will be `true`, so that we can perform the redirect manually to the new URL (if needed).

## integrity

The `integrity` option allows to check if the response matches the known-ahead checksum.

As described in the [specification](https://w3c.github.io/webappsec-subresource-integrity/), supported hash-functions are SHA-256, SHA-384, and SHA-512, there might be others depending on a browser.

For example, we're downloading a file, and we know that it's SHA-256 checksum is "abc" (a real checksum is longer, of course).

We can put it in the `integrity` option, like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
fetch('http://site.com/file', {
  integrity: 'sha256-abd'
});
```

<<<<<<< HEAD
すると、`fetch` は自身で SHA-256 を計算し、文字列比較をします。一致しない場合はエラーが発生します。

## keepalive

`keepalive` オプションは、リクエストがページよりも長生きする可能性があること意味します。

例えば、ユーザ体験を向上させるために、現在の訪問者がどのように我々のページを使用しているか(マウスクリック、閲覧したページの断片 など)に関する統計を収集するとします。

訪問者がページを離れるとき -- それをサーバ上に保存したいです。

`window.onunload` を使用すると実現できます:
=======
Then `fetch` will calculate SHA-256 on its own and compare it with our string. In case of a mismatch, an error is triggered.

## keepalive

The `keepalive` option indicates that the request may outlive the page.

For example, we gather statistics about how the current visitor uses our page (mouse clicks,  page fragments he views), to improve user experience.

When the visitor leaves our page -- we'd like to save it on our server.

We can use `window.onunload` for that:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js run
window.onunload = function() {
  fetch('/analytics', {
    method: 'POST',
    body: "statistics",
*!*
    keepalive: true
*/!*
  });
};
```

<<<<<<< HEAD
通常、ドキュメントがアンロードされると、関連するすべてのネットワークリクエストは中止されます。しかし `keepalive` オプションは、たとえページから離れた後だとしてもバックグランドでそれを実行するようブラウザに指示します。そのため、リクエストが成功するためにはこれは不可欠です。

- メガバイトを送信することはできません: keepalive リクエストの場合の本文の制限は 64kb です。
    - もしもより多くのデータを集める場合は、定期的にそれを送ります。そうすれば、"onunload" 時のリクエストは多くはならないでしょう。
    - この制限は、現在進行中のすべてのリクエストに対するものです。なので、それぞれ 64kb のリクエストを 100 個作成することで騙すことができます。
- リクエストが `onunload` で行われた場合、サーバの応答は得られません。なぜならドキュメントはその時点ですでにアンロードされているからです。
    - 通常、サーバはこのようなリクエストに対しては空のレスポンスを返すので問題はありません。
=======
Normally, when a document is unloaded, all associated network requests are aborted. But `keepalive` option tells the browser to perform the request in background, even after it leaves the page. So it's essential for our request to succeed.

- We can't send megabytes: the body limit for keepalive requests is 64kb.
    - If we gather more data, we can send it out regularly, then there won't be a lot for the "onunload" request.
    - The limit is for all currently ongoing requests. So we cheat it by creating 100 requests, each 64kb.
- We don't get the server response if the request is made `onunload`, because the document is already unloaded at that time.
    - Usually, the server sends empty response to such requests, so it's not a problem.
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
