このタスクの HTML は正しくありません。これが奇妙な事象の理由です。

ブラウザはそれを自動的に修正する必要があります。しかし、`<table>` の中にテキストはないかもしれません。: 仕様によると、テーブル固有のタグだけが許可されます。したがって、ブラウザは `<table>` の *前に* `"aaa"` を追加します。

これで、テーブルを削除したときに文字列が残っていた理由は明白になりました。

<<<<<<< HEAD
この問題はブラウザツールを使ってDOMを調べると簡単に答えることができます。`<table>` の前に `"aaa"` があります。
=======
The question can be easily answered by exploring the DOM using the browser tools. It shows `"aaa"` before the `<table>`.
>>>>>>> 97ef86242f9f236b13152e1baf52a55c4db8728a

HHTML標準では、悪いHTMLを処理する方法を詳細に指定しています。このようなブラウザの動作は正しいです。
