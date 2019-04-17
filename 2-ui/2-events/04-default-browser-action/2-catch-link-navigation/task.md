importance: 5

---

# 要素内のリンクをキャッチする

<<<<<<< HEAD
`id="contents"` の要素内のすべてのリンクが、ユーザに本当に離れたいかを尋ねるようにしてください。そして、答えが No の場合は遷移しません。
=======
Make all links inside the element with `id="contents"` ask the user if they really want to leave. And if they don't then don't follow.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

このようになります:

[iframe height=100 border=1 src="solution"]

詳細:

- 要素内の HTML はロードされているかもしれないし、いつでも動的に再作成されるかもしれません。そのため、すべてのリンクを見つけてハンドラを配置することはできません。イベントの移譲を使ってください。
- コンテンツはネストされたタグを持っている場合があります。リンクも同じです。 `<a href=".."><i>...</i></a>`.
