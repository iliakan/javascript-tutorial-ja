importance: 4

---

# '?' または '||' を使って関数を書き直す


次の関数は、パラメータ `age` が `18` より大きい場合に `true` を返します。

それ以外の場合には確認を行い、その結果を返します。:

```js
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('Do you have your parents permission to access this page?');
  }
}
```

それを書き直し、1行で `if` なしで同じをことを実行してください。

`checkAge` の2つのバリアントを作ってください。:

<<<<<<< HEAD
1. 疑問符演算子 `'?'` を使うケース
2. OR `||` を使うケース
=======
1. Using a question mark operator `?`
2. Using OR `||`
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613
