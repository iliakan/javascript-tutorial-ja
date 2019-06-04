<<<<<<< HEAD
# Fetch: クロスオリジン(Cross-Origin) リクエスト

もし任意の web サイトから `fetch` を行った場合、そのリクエストは恐らく失敗するでしょう。

ここで中心となる概念は *オリジン* -- ドメイン/ポート/プロトコルの３つ揃いです。 

クロスオリジンリクエスト(これらは別のドメイン(サブドメインも)、プロトコル、あるいはポートに送信されたもの)には、リモート側からの特別なヘッダが必要です。そのポリシーは "CORS" (Cross-Origin Resource Sharing) と呼ばれています。

例えば、`http://example.com` へのフェッチをしてみましょう。:
=======
# Fetch: Cross-Origin Requests

If we make a `fetch` from an arbitrary web-site, that will probably fail.

The core concept here is *origin* -- a domain/port/protocol triplet.

Cross-origin requests -- those sent to another domain (even a subdomain) or protocol or port -- require special headers from the remote side. That policy is called "CORS": Cross-Origin Resource Sharing.

For instance, let's try fetching `http://example.com`:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js run async
try {
  await fetch('http://example.com');
} catch(err) {
  alert(err); // Failed to fetch
}
```

<<<<<<< HEAD
予想通り、fetch は失敗します。

## なぜ?

なぜなら、クロスオリジン制約が悪意のあるハッカーからインターネットを保護するからです。

脱線しますが、簡単に歴史的な背景を振り返りましょう。

長い間、JavaScript はネットワークリクエストを実行するための特別なメソッドを持っていませんでした。

**あるサイトのスクリプトが別のサイトのコンテンツへアクセスすることはできませんでした。**

このシンプルだけど強力なルールはインターネットセキュリティの基盤でした。例えば、ページ `hacker.com` のスクリプトは `gmail.com` にあるユーザのメールボックにはアクセスできませんでした。ユーザはそれを安全と思いました。

しかし、web 開発者はより強力な力を求めました。そしてそれを回避するための様々なトリックが考案されました。

別のサーバとやり取りする方法の１つは、そこに `<form>` を送信することでした。次のように、現在のページに留まるために `<iframe>` に送信しました。:
=======
Fetch fails, as expected.

## Why?

Because cross-origin restrictions protect the internet from evil hackers.

Seriously. Let's make a very brief historical digression.

For many years JavaScript did not have any special methods to perform network requests.

**A script from one site could not access the content of another site.**

That simple, yet powerful rule was a foundation of the internet security. E.g. a script from the page `hacker.com` could not access user's mailbox at `gmail.com`. People felt safe.

But web developers demanded more power. A variety of tricks were invented to work around it.

One way to communicate with another server was to submit a `<form>` there. People submitted it into `<iframe>`, just to stay on the current page, like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```html
<!-- form target -->
<iframe name="iframe"></iframe>

<<<<<<< HEAD
<!-- JavaScript により form は動的に生成され、サブミットされました -->
=======
<!-- a form could be dynamically generated and submited by JavaScript -->
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
<form target="iframe" method="POST" action="http://another.com/…">
  ...
</form>

```

<<<<<<< HEAD
- これにより、ネットワーキングのメソッドがなくても、別のサイトへ GET/POST リクエストを送ることは可能でした。
- しかし、別のサイトから `<iframe>` のコンテンツにアクセスすることは禁止されているので、レスポンスを読むことはできませんでした。

したがって、`<form>` はどこにでもデータをサブミットすることを可能にしましたが、レスポンスのコンテンツにはアクセスできませんでした。

別の方法は `<script src="http://another.com/…">` タグを使用することでした。スクリプトは任意のドメインの `src` を持つことができます。しかし、改めて -- このようなスクリプトの生のコンテンツにアクセスすることは不可能でした。

もし `another.com` がこのような種類のアクセスに対してデータを公開するつもりだった場合、いわゆる "JSONP (JSPN with padding)" プロトコルが使われました。

これはそのフローです:

1. まず、事前に e.g. `gotWeather` のような、データを受け取るためのグローバル関数を宣言します。
2. 次に `<script>` を作り、その名前を `callback` クエリーパラメータとして渡します。e.g. `src="http://another.com/weather.json?callback=gotWeather"`.
3. リモートサーバは、データを `gotWeather(...)` 呼び出しにラップするようなレスポンスを動的に生成します。
4. スクリプトが実行されると、`gotWeather` が実行されデータが得られます。

これは JSONP でデータを受け取るコードの例です:

```js run
// 1. データを処理する関数を宣言します
=======
- So, it was possible to make a GET/POST request to another site, even without networking methods.
- But as it's forbidden to access the content of an `<iframe>` from another site, it wasn't possible to read the response.

So, `<form>` allowed to submit the data anywhere, but the response content was unaccessible.

Another trick was to use a `<script src="http://another.com/…">` tag. A script could have any `src`, from any domain. But again -- it was impossible to access the raw content of such script.

If `another.com` intended to expose data for this kind of access, then a so-called "JSONP (JSON with padding)" protocol was used.

Here's the flow:

1. First, in advance, we declare a global function to accept the data, e.g. `gotWeather`.
2. Then we make a `<script>` and pass its name as the `callback` query parameter, e.g. `src="http://another.com/weather.json?callback=gotWeather"`.
3. The remote server dynamically generates a response that wraps the data into `gotWeather(...)` call.  
4. As the script executes, `gotWeather` runs, and, as it's our function, we have the data.

Here's an example of the code to receive the data in JSONP:

```js run
// 1. Declare the function to process the data
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
function gotWeather({ temperature, humidity }) {
  alert(`temperature: ${temperature}, humidity: ${humidity}`);
}

<<<<<<< HEAD
// 2. スクリプトに対して、?callback パラメータとしてその名前を渡します
=======
// 2. Pass its name as the ?callback parameter for the script
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
let script = document.createElement('script');
script.src = `https://cors.javascript.info/article/fetch-crossorigin/demo/script?callback=gotWeather`;
document.body.append(script);

<<<<<<< HEAD
// 3. サーバから期待する応答は次のようになります:
=======
// 3. The expected answer from the server looks like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
/*
gotWeather({
  temperature: 25,
  humidity: 78
});
*/
```

<<<<<<< HEAD
これは動作し、セキュリティにも違反しません。なぜなら、双方がこの方法でデータを渡すことに合意しているからです。双方が合意するときはハックではありません。これは非常に古いブラウザでも動作するため、このようなアクセスを提供するサービスはまだ存在します。

しばらくすると、現在のネットワークメソッドが登場しました。当初はクロスオリジンリクエストは禁止されていました。しかし、長い議論の結果、サーバによって明示的に許可されている場合に限り、クロスオリジンリクエストは許可されました。

## 単純リクエスト(Simple requests)

[Simple requests](http://www.w3.org/TR/cors/#terminology) は次の条件を満たす必要があります。:

1. [Simple method](http://www.w3.org/TR/cors/#simple-method): GET, POST または HEAD
2. [Simple headers](http://www.w3.org/TR/cors/#simple-header) -- 許可されているものだけ(以下):
    - `Accept`,
    - `Accept-Language`,
    - `Content-Language`,
    - 値が `application/x-www-form-urlencoded`, `multipart/form-data` あるいは `text/plain` の `Content-Type`.

その他のリクエストは "単純ではない(non-simple)" とみなされます。例えば、`PUT` メソッドや、 `API-Key` HTTP ヘッダを持つリクエストはこれに限りません。

**本質的な違いは、"単純リクエスト" は、特別な方法を使うことなく `<form>` または `<script>` を使って作成することができることです。**

そのため、たとえ非常に古いサーバでも、単純リクエストを受け入れる準備ができているはずです。

逆に、非標準のヘッダ、あるいは例えば `DELETE` メソッドのリクエストはこの方法では作ることはできません。長い間、JavaScript はこのようなリクエストを行うことができませんでした。なので、古いサーバは、そのようなリクエストは特権のある送信元から来たものであると想定する場合があります(web ページではそのようなリクエストは送信できないため)。

単純でないリクエストをしようとすろと、ブラウザは特別な "preflight" リクエストを送信します。これは、サーバにこのようなクロスオリジンリクエストを受け入れることに同意するか否かを尋ねるものです。

そして、サーバがヘッダで明示的にそれを確認しない限り、単純でないリクエストは送信されません。

それでは詳細に進みましょう。これらはすべて1つの目的のためにあります。それは、新しいクロスオリジンの機能がサーバからの明示的な許可がある場合にのみアクセス可能であることを保証するためです。

## 単純リクエストに対する CORS

リクエストがクロスオリジンである場合、ブラウザは常に `Origin` ヘッダを追加します。

例えば、`https://javascript.info/page` から `https://anywhere.com/request` にリクエストを行う場合、ヘッダは次のようになるでしょう:
=======

That works, and doesn't violate security, because both sides agreed to pass the data this way. And, when both sides agree, it's definitely not a hack. There are still services that provide such access, as it works even for very old browsers.

After a while, modern network methods appeared. At first, cross-origin requests were forbidden. But as a result of long discussions, cross-domain requests were  allowed, in a way that does not add any capabilities unless explicitly allowed by the server.

## Simple requests

[Simple requests](http://www.w3.org/TR/cors/#terminology) must satisfy the following conditions:

1. [Simple method](http://www.w3.org/TR/cors/#simple-method): GET, POST or HEAD
2. [Simple headers](http://www.w3.org/TR/cors/#simple-header) -- only allowed:
    - `Accept`,
    - `Accept-Language`,
    - `Content-Language`,
    - `Content-Type` with the value `application/x-www-form-urlencoded`, `multipart/form-data` or `text/plain`.

Any other request is considered "non-simple". For instance, a request with `PUT` method or with an `API-Key` HTTP-header does not fit the limitations.

**The essential difference is that a "simple request" can be made with a `<form>` or a `<script>`, without any special methods.**

So, even a very old server should be ready to accept a simple request.

Contrary to that, requests with non-standard headers or e.g. method `DELETE` can't be created this way. For a long time JavaScript was unable to do such requests. So an old server may assume that such requests come from a privileged source, "because a webpage is unable to send them".

When we try to make a non-simple request, the browser sends a special "preflight" request that asks the server -- does it agree to accept such cross-origin requests, or not?

And, unless the server explicitly confirms that with headers, a non-simple request is not sent.

Now we'll go into details. All of them serve a single purpose -- to ensure that new cross-origin capabilities are only accessible with an explicit permission from the server.

## CORS for simple requests

If a request is cross-origin, the browser always adds `Origin` header to it.

For instance, if we request `https://anywhere.com/request` from `https://javascript.info/page`, the headers will be like:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
GET /request
Host: anywhere.com
*!*
Origin: https://javascript.info
*/!*
...
```

<<<<<<< HEAD
ご覧の通り、`Origin` はパスなしの正確なオリジン(ドメイン/プロトコル/ポート)を含みます。

サーバは `Origin` を検査することができ、このようなリクエストを受け入れることに同意すると、レスポンスに `Access-Control-Allow-Origin` という特別なヘッダを追加します。このヘッダは許可されたオリジン(このケースでは `https://javascript.info`)、あるいはアスタリスク `*` を含む必要があります。そして応答は成功します。そうでなければエラーになります。

ブラウザはここでは信頼された仲介者の役割を果たします。:
1. 正しい `Origin` がクロスドメインリクエストと一緒に送信されることを保証します。
2. レスポンスの中で正しい `Access-Control-Allow-Origin` を確認すると、次は JavaScript アクセス、そうでなければエラーと共に禁止します。

![](xhr-another-domain.png)

これは "受け入れに同意した" 応答の例です:
=======
As you can see, `Origin` contains exactly the origin (domain/protocol/port), without a path.

The server can inspect the `Origin` and, if it agrees to accept such a request, adds a special header `Access-Control-Allow-Origin` to the response. That header should contain the allowed origin (in our case `https://javascript.info`), or a star `*`. Then the response is successful, otherwise an error.

The browser plays the role of a trusted mediator here:
1. It ensures that the corrent `Origin` is sent with a cross-domain request.
2. If checks for correct `Access-Control-Allow-Origin` in the response, if it is so, then JavaScript access, otherwise forbids with an error.

![](xhr-another-domain.png)

Here's an example of an "accepting" response:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
```
200 OK
Content-Type:text/html; charset=UTF-8
*!*
Access-Control-Allow-Origin: https://javascript.info
*/!*
```

<<<<<<< HEAD
## レスポンスヘッダ

クロスオリジンリクエストの場合、デフォルトでは JavaScript は "単純レスポンスヘッダ" にしかアクセスできません。:
=======
## Response headers

For cross-origin request, by default JavaScript may only access "simple response headers":
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

- `Cache-Control`
- `Content-Language`
- `Content-Type`
- `Expires`
- `Last-Modified`
- `Pragma`

<<<<<<< HEAD
他のレスポンスヘッダは禁止されています。

```smart header="注意してください: `Content-Length` はありません"
注意: 上のリストに `Content-Length` ヘッダはありません!

そのため、何かをダウンロードしていて進捗具合を追跡したい場合は、ヘッダにアクセスするために追加の許可が必要になります(下記参照)。
```

JavaScript が他のレスポンスヘッダへアクセスするのを許可するには、サーバは `Access-Control-Expose-Headers` ヘッダに、アクセスを許可するヘッダをリストする必要があります。

例:
=======
Any other response header is forbidden.

```smart header="Please note: no `Content-Length`"
Please note: there's no `Content-Length` header in the list!

So, if we're downloading something and would like to track the percentage of progress, then an additional permission is required to access that header (see below).
```

To grant JavaScript access to any other response header, the server must list it in the `Access-Control-Expose-Headers` header.

For example:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
200 OK
Content-Type:text/html; charset=UTF-8
Content-Length: 12345
API-Key: 2c9de507f2c54aa1
Access-Control-Allow-Origin: https://javascript.info
*!*
Access-Control-Expose-Headers: Content-Length,API-Key
*/!*
```

<<<<<<< HEAD
このような `Access-Control-Expose-Headers` ヘッダを使うことで、スクリプトが `Content-Length` と `API-Key` ヘッダにアクセスすることを許可します。


## "単純ではない" リクエスト

私たちは単なる `GET/POST` だけでなく、`PATCH` や `DELETE` などの HTTP メソッドを使うことができます。

以前は web ページがこのようなリクエストを行うことができるとは、誰も想定していませんでした。そのため、標準ではないメソッドを "ブラウザではない" という合図として扱う web サービスが存在する可能性があります。They can take it into account when checking access rights.

そのため、解釈違いを避けるために、昔は扱えなかった "単純ではない" リクエストについては、ブラウザはすぐにはこのようなリクエストを行いません。その前に、許可を求めるための準備的な、いわゆる "preflight" リクエストを送信します。

preflight リクエストは `OPTIONS` メソッドを使い、本文はありません。
- `Access-Control-Request-Method` ヘッダは要求されたメソッドを持ちます。
- `Access-Control-Request-Headers` ヘッダは単純でない HTTP ヘッダのカンマ区切りのリストを提供します。

サーバがリクエストを処理するのに同意する場合、ステータス 200 で本文なしの応答を返します。

- レスポンスヘッダ `Access-Control-Allow-Methods` は許可されたメソッドを持たなければなりません。
- レスポンスヘッダ `Access-Control-Allow-Headers` は許可されたヘッダのリストを持たなければなりません。
- 加えて、ヘッダ `Access-Control-Max-Age` でパーミッションキャッシュする秒数を指定する場合があります。その場合、ブラウザは与えれたパーミッションを満たす後続のリクエストに対して preflight を送信する必要はありません。

![](xhr-preflight.png)

クロスドメインの `PATCH` リクエストの例でステップ毎にどのように動作するのか見ていきましょう(このメソッドはデータを更新するのによく使われます)。:
=======
With such `Access-Control-Expose-Headers` header, the script is allowed to access `Content-Length` and `API-Key` headers of the response.


## "Non-simple" requests

We can use any HTTP-method: not just `GET/POST`, but also `PATCH`, `DELETE` and others.

Some time ago no one could even assume that a webpage is able to do such requests. So there may exist webservices that treat a non-standard method as a signal: "That's not a browser". They can take it into account when checking access rights.

So, to avoid misunderstandings, any "non-simple" request -- that couldn't be done in the old times, the browser does not make such requests right away. Before it sends a preliminary, so-called "preflight" request, asking for permission.

A preflight request uses method `OPTIONS` and has no body.
- `Access-Control-Request-Method` header has the requested method.
- `Access-Control-Request-Headers` header provides a comma-separated list of non-simple HTTP-headers.

If the server agrees to serve the requests, then it should respond with status 200, without body.

- The response header `Access-Control-Allow-Methods` must have the allowed method.
- The response header `Access-Control-Allow-Headers` must have a list of allowed headers.
- Additionally, the header `Access-Control-Max-Age` may specify a number of seconds to cache the permissions. So the browser won't have to send a preflight for subsequent requests that satisfy given permissions.

![](xhr-preflight.png)

Let's see how it works step-by-step on example, for a cross-domain `PATCH` request (this method is often used to update data):
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
let response = await fetch('https://site.com/service.json', {
  method: 'PATCH',
  headers: {
    'Content-Type': 'application/json'  
    'API-Key': 'secret'
  }
});
```

<<<<<<< HEAD
リクエストが単純でない理由が3つあります:
- メソッドが `PATCH`
- `Content-Type` は次のいずれでもない: `application/x-www-form-urlencoded`, `multipart/form-data`,  `text/plain`.
- カスタムの `API-Key` ヘッダ.

### Step 1 (preflight リクエスト)

ブラウザは自身で次のような preflight リクエストを投げます:
=======
There are three reasons why the request is not simple (one is enough):
- Method `PATCH`
- `Content-Type` is not one of: `application/x-www-form-urlencoded`, `multipart/form-data`,  `text/plain`.
- Custom `API-Key` header.

### Step 1 (preflight request)

The browser, on its own, sends a preflight request that looks like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
OPTIONS /service.json
Host: site.com
Origin: https://javascript.info
Access-Control-Request-Method: PATCH
Access-Control-Request-Headers: Content-Type,API-Key
```

<<<<<<< HEAD
- メソッド: `OPTIONS`.
- パス -- メインのリクエストと正確に同じ: `/service.json`.
- クロスオリジンの特別なヘッダ:
    - `Origin` -- 送信元のオリジン.
    - `Access-Control-Request-Method` -- リクエストされたメソッド
    - `Access-Control-Request-Headers` -- カンマ区切りの "単純ではない" ヘッダのリスト

### Step 2 (preflight レスポンス)

サーバはステータス 200 と 次のヘッダを応答する必要があります:
- `Access-Control-Allow-Methods: PATCH`
- `Access-Control-Allow-Headers: Content-Type,API-Key`.

これは今後のやり取りを許可します。そうでなければ、エラーが起きるでしょう。

サーバが他のメソッドとヘッダも待ち受けている場合、一度にそれらすべてをリストするのは理にかなっています。例:
=======
- Method: `OPTIONS`.
- The path -- exactly the same as the main request: `/service.json`.
- Cross-origin special headers:
    - `Origin` -- the source origin.
    - `Access-Control-Request-Method` -- requested method.
    - `Access-Control-Request-Headers` -- a comma-separated list of "non-simple" headers.

### Step 2 (preflight response)

The server should respond with status 200 and headers:
- `Access-Control-Allow-Methods: PATCH`
- `Access-Control-Allow-Headers: Content-Type,API-Key`.

That would allow future communication, otherwise an error is triggered.

If the server expects other methods and headers, makes sense to list them all at once, e.g:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
200 OK
Access-Control-Allow-Methods: PUT,PATCH,DELETE
Access-Control-Allow-Headers: API-Key,Content-Type,If-Modified-Since,Cache-Control
Access-Control-Max-Age: 86400
```

<<<<<<< HEAD
これでブラウザは `PATCH` が許可されたメソッドのリストにあり、両方のヘッダもリストにあるこが確認できたので、メインのリクエストを送信します。

加えて、preflight レスポンスは `Access-Control-Max-Age` ヘッダで指定された時間(86400 秒, 1日)キャッシュされます。そのため後続のリクエストでは preflight は起きません。それらはキャッシュの内容から許容と想定して、直接送信されます。

### Step 3 (実際のリクエスト)

preflight が成功すると、ブラウザは本当のリクエストを行います。ここでのフローは単純リクエストの場合と同じです。

実際のリクエストは `Origin` ヘッダを持ちます(クロスオリジンのため)。:
=======
Now the browser can see that `PATCH` is in the list of allowed methods, and both headers are in the list too, so it sends out the main request.

Besides, the preflight response is cached for time, specified by `Access-Control-Max-Age` header (86400 seconds, one day), so subsequent requests will not cause a preflight. Assuming that they fit the allowances, they will be sent directly.

### Step 3 (actual request)

When the preflight is successful, the browser now makes the real request. Here the flow is the same as for simple requests.

The real request has `Origin` header (because it's cross-origin):
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
PATCH /service.json
Host: site.com
Content-Type: application/json
API-Key: secret
Origin: https://javascript.info
```

<<<<<<< HEAD
### Step 4 (実際のレスポンス)

サーバは `Access-Control-Allow-Origin` をレスポンスに追加するのを忘れないでください。それがないと、成功した preflight は解放しません。:
=======
### Step 4 (actual response)

The server should not forget to add `Access-Control-Allow-Origin` to the response. A successful preflight does not relieve from that:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
Access-Control-Allow-Origin: https://javascript.info
```

<<<<<<< HEAD
これですべてOKです。JavaScript は完全なレスポンスを読むことができます。
=======
Now everything's correct. JavaScript is able to read the full response.
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb


## Credentials

<<<<<<< HEAD
デフォルトでは、クロスオリジンリクエストはクレデンシャル(cookie or HTTP 認証)を持ちません。

これは HTTP リクエストでは一般的ではありません。通常 `http://site.com` へのリクエストはそのドメインのすべての cookie を伴います。しかし、JavaScript メソッドにより作られたクロスオリジンリクエストは例外です。

例えば、`fetch('http://another.com')` は cookie を送信しません。たとえ `another.com` ドメインに属するものであっても。

なぜでしょう?

なぜなら、クレデンシャルを持つリクエストは匿名のリクエストよりもはるかに強力だからです。もし許可されていると、それは JavaScript にユーザに代わって機密情報にアクセスする全権限を与えることになります。

サーバは本当に `Origin` のページをそれほど信頼しているのでしょうか？クレデンシャルを持つリクエストが通過するための追加のヘッダが必要です。

クレデンシャルを有効にするには、オプション `credentials: "include"` を追加します。:
=======
A cross-origin request by default does not bring any credentials (cookies or HTTP authentication).

That's uncommon for HTTP-requests. Usually, a request to `http://site.com` is accompanied by all cookies from that domain. But cross-domain requests made by JavaScript methods are an exception.

For example, `fetch('http://another.com')` does not send any cookies, even those that belong to `another.com` domain.

Why?

That's because a request with credentials is much more powerful than an anonymous one. If allowed, it grants JavaScript the full power to act and access sensitive information on behalf of a user.

Does the server really trust pages from `Origin` that much? A request with credentials needs an additional header to pass through.

To enable credentials, we need to add the option `credentials: "include"`, like this:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
fetch('http://another.com', {
  credentials: "include"
});
```

<<<<<<< HEAD
これで `fetch` はリクエストと一緒に `another.com` からの cookie を送信します。

もしサーバがクレデンシャルを含むリクエストを受け入れたい場合は、`Access-Control-Allow-Origin` に加えて、レスポンスにヘッダ `Access-Control-Allow-Credentials: true` を追加する必要があります。

例:
=======
Now `fetch` sends cookies originating from `another.com` with the request.

If the server wishes to accept the request with credentials, it should add a header `Access-Control-Allow-Credentials: true` to the response, in addition to `Access-Control-Allow-Origin`.

For example:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```
200 OK
Access-Control-Allow-Origin: https://javascript.info
Access-Control-Allow-Credentials: true
```

<<<<<<< HEAD
注意してください: `Access-Control-Allow-Origin` はクレデンシャルを持つリクエストに対してアスタリスク `*` を使うことは禁止されています。上のように正確なオリジンでなければなりません。これはサーバが本当に信頼する相手を知っていることを保証するための追加の安全対策です。

## サマリ

ネットワークメソッドはクロスオリジンリクエストを2種類に分けます: "単純" とその他です。

[単純リクエスト](http://www.w3.org/TR/cors/#terminology) は次の条件を満たさなければなりません:
- メソッド: GET, POST or HEAD.
- ヘッダ -- 次のものだけセットできます:
    - `Accept`
    - `Accept-Language`
    - `Content-Language`
    - `Content-Type`: `application/x-www-form-urlencoded`, `multipart/form-data` または `text/plain` のいずれか.

本質的な違いは、単純リクエストは以前から `<form>` もしくは `<script>` タグを使用して行うことができました。その一方、単純でないものは、ブラウザでは長い間不可能だったことです。

実際の違いは、単純リクエストは `Origin` ヘッダとともにすぐに送信されますが、他のリクエストでは、ブラウザは許可を求めるために事前の "priflight" リクエストを行います。

**単純リクエストの場合:**

- → ブラウザは送信元をもつ `Origin` ヘッダを送信します。
- ← クレデンシャルを持たないリクエストの場合(デフォルト)、サーバは以下を設定する必要があります:
    - `Access-Control-Allow-Origin` に `*` または `Origin` と同じ値
- ← クレデンシャルを持つリクエストの場合、サーバは以下を設定する必要があります:
    - `Access-Control-Allow-Origin` に `Origin`
    - `Access-Control-Allow-Credentials` に `true`

さらに、JavaScript で単純でないレスポンスヘッダ(下記以外)にアクセスしたい場合:
=======
Please note: `Access-Control-Allow-Origin` is prohibited from using a star `*` for requests with credentials. There must be exactly the origin there, like above. That's an additional safety measure, to ensure that the server really knows who it trusts.


## Summary

Networking methods split cross-origin requests into two kinds: "simple" and all the others.

[Simple requests](http://www.w3.org/TR/cors/#terminology) must satisfy the following conditions:
- Method: GET, POST or HEAD.
- Headers -- we can set only:
    - `Accept`
    - `Accept-Language`
    - `Content-Language`
    - `Content-Type` to the value `application/x-www-form-urlencoded`, `multipart/form-data` or `text/plain`.

The essential difference is that simple requests were doable since ancient times using `<form>` or `<script>` tags, while non-simple were impossible for browsers for a long time.

So, practical difference is that simple requests are sent right away, with `Origin` header, but for other ones the browser makes a preliminary "preflight" request, asking for permission.

**For simple requests:**

- → The browser sends `Origin` header with the origin.
- ← For requests without credentials (default), the server should set:
    - `Access-Control-Allow-Origin` to `*` or same as `Origin`
- ← For requests with credentials, the server should set:
    - `Access-Control-Allow-Origin` to `Origin`
    - `Access-Control-Allow-Credentials` to `true`

Additionally, if JavaScript wants to access non-simple response headers:
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
- `Cache-Control`
- `Content-Language`
- `Content-Type`
- `Expires`
- `Last-Modified`
- `Pragma`

<<<<<<< HEAD
...サーバは許可されたものを `Access-Control-Expose-Headers` ヘッダにリストする必要があります。

**単純でないリクエストの場合、要求されたものの前に事前の "preflight" リクエストが発行されます。**

- → ブラウザは次のヘッダと共に同じ URL に `OPTIONS` リクエストを送信します。:
    - `Access-Control-Request-Method` は要求されたメソッドを持ちます
    - `Access-Control-Request-Headers` は要求された単純でないヘッダのリストです
- ← サーバはステータス 200 と次のヘッダを応答します:
    - `Access-Control-Allow-Methods` は許可されたメソッドのリストを含みます,
    - `Access-Control-Allow-Headers` は許可されたヘッダのリストを含みます,
    - `Access-Control-Max-Age` は許可(パーミッション)のキャッシュの秒数です。
- その後、実際のリクエストが送信され、前の "単純な" スキームが適用されます。
=======
...Then the server should list the allowed ones in `Access-Control-Expose-Headers` header.

**For non-simple requests, a preliminary "preflight" request is issued before the requested one:**

- → The browser sends `OPTIONS` request to the same url, with headers:
    - `Access-Control-Request-Method` has requested method.
    - `Access-Control-Request-Headers` lists non-simple requested headers
- ← The server should respond with status 200 and headers:
    - `Access-Control-Allow-Methods` with a list of allowed methods,
    - `Access-Control-Allow-Headers` with a list of allowed headers,
    - `Access-Control-Max-Age` with a number of seconds to cache permissions.
- Then the actual request is sent, the previous "simple" scheme is applied.
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb
