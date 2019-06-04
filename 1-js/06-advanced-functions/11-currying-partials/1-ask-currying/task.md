importance: 5

---

# ログイン用の部分的なアプリケーション

このタスクは <info:task/question-use-bind> 少しより複雑なバリアントです。  

`user` オブジェクトが修正されました。今、2つの関数 `loginOk/loginFail` の代わりに、単一の関数 `user.login(true/false)` があります。

<<<<<<< HEAD
下のコードでは、何を渡すと `ok` として `user.login(true)` を、`fail` として `user.login(fail)` を呼ぶでしょうか？
=======
What to pass `askPassword` in the code below, so that it calls `user.login(true)` as `ok` and `user.login(false)` as `fail`?
>>>>>>> a0266c574c0ab8a0834dd38ed65e7e4ee27f9cdb

```js
function askPassword(ok, fail) {
  let password = prompt("Password?", '');
  if (password == "rockstar") ok();
  else fail();
}

let user = {
  name: 'John',

  login(result) {
    alert( this.name + (result ? ' logged in' : ' failed to log in') );
  }
};

*!*
askPassword(?, ?); // ?
*/!*
```

変更はハイライトされた箇所の修正だけにしてください。

