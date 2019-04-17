importance: 3

---

# ログインのチェック

`prompt` でログインを要求するコードを書いてください。

もし訪問者が `"Admin"` と入力したら、パスワードのための `prompt` を出します。もし入力が空行または `key:Esc` の場合 -- "Canceled" と表示します。別の文字列の場合は -- "I don't know you" と表示します。

パスワードは次に沿ってチェックされます:

- ”TheMaster" と等しい場合には "Welcome!" と表示します。
- 別の文字列の場合 -- "Wrong password" を表示します。
- 空文字または入力がキャンセルされた場合には "Canceled." と表示します。


図:

![](ifelse_task.png)

入れ子の `if` ブロックを使ってください。コードの全体的な読みやすさに気をつけてください。

Hint:  passing an empty input to a prompt returns an empty string `''`. Pressing `key:ESC` during a prompt returns `null`.

[demo]
