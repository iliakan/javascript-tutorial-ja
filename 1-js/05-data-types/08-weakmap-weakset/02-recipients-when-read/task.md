importance: 5

---

# 読んだ日付を格納する

[前のタスク](info:task/recipients-read)のメッセージ配列があります。状況は似ています。

```js
let messages = [
  {text: "Hello", from: "John"},
  {text: "How goes?", from: "John"},
  {text: "See you soon", from: "Alice"}
];
```

この問題: "いつメッセージが読まれたか" という情報を格納するのにあなたが提案するのはどのようなデータ構造ですか？

<<<<<<< HEAD:1-js/05-data-types/07-map-set-weakmap-weakset/05-recipients-when-read/task.md
前のタスクでは、"既読/未読" の事実の保持だけが必要でした。今度は日付を保存する必要があります。なお、前と同じようにメッセージが削除されたら現れないでください。
=======
In the previous task we only needed to store the "yes/no" fact. Now we need to store the date, and it should only remain in memory until the message is garbage collected.

P.S. Dates can be stored as objects of built-in `Date` class, that we'll cover later.
>>>>>>> fb38a13978f6e8397005243bc13bc1a20a988e6a:1-js/05-data-types/08-weakmap-weakset/02-recipients-when-read/task.md