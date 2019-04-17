# マウスイベントでのドラッグ&ドロップ

ドラッグ&ドロップは素晴らしいインタフェースソリューションです。何かを掴み、ドラッグとドロップをすることは、コピーや移動(ファイルマネージャを参照)から注文(カートにドロップする)まで、多くのことをするための明白かつ簡単な方法です。

現在の HTML 標準では [ドラッグイベントに関するセクション](https://html.spec.whatwg.org/multipage/interaction.html#dnd) があります。

それらはシンプルなタスクを簡単に解決したり、"外部" ファイルのドラッグ＆ドロップをブラウザで扱うことができたりと、興味深いです。したがって、OSのファイルマネージャでファイルを取り、ブラウザウィンドウへドロップすることができます。その後、JavaScript はそのコンテンツへアクセスできます。

しかし、ネイティブのドラッグイベントにも制限があります。例えば、特定の領域でドラッグを制限することができます。また、ドラッグを "水平" または "垂直" のみにすることはできません。そのAPIでは実装できない他のドラッグ&ドロップのタスクがあります。

そのため、ここではマウスイベントを使用したドラッグ&ドロップの実装方法を見ていきます。それほど難しくはありません。

## ドラッグ&ドロップ アルゴリズム 

基本のドラッグ&ドロップのアルゴリズムはこのようになります:

<<<<<<< HEAD
1. ドラッグ可能な要素で `mousedown` をキャッチします。
2. 移動する要素を準備します (そのコピーを作成したりなど)
3. その後、`mousemove` で `left/top` と `position:absolute` を変更することで、それを移動させます。
4. `mouseup` (ボタンを離す) で、 -- 終了したドラッグ&ドロップに関連するすべてのアクションを実行します。
=======
1. Catch `mousedown` on a draggable element.
2. Prepare the element for moving (maybe create a copy of it or whatever).
3. Then on `mousemove` move it by changing `left/top` and `position:absolute`.
4. On `mouseup` (button release) -- perform all actions related to a finished Drag'n'Drop.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

これらは基本です。私たちはそれを拡張することができます。例えば、ドロップ可能な要素上にマウスを持ってきたときに、それを強調表示するなどです。

ここでは、ボールのドラッグ&ドロップの場合のアルゴリズムです:

```js
ball.onmousedown = function(event) { // (1) 処理を開始

  // (2) 移動のための準備: absolute にし、z-index でトップにする
  ball.style.position = 'absolute';
  ball.style.zIndex = 1000;
  // 現在の親から body へ直接移動させ、body に対して相対配置をする
  document.body.append(ball);  
  // ...そしてその絶対配置されたボールをカーソルの下に置く

  moveAt(event.pageX, event.pageY);

  // ボールを（pageX、pageY）座標の中心に置く
  function moveAt(pageX, pageY) {
    ball.style.left = pageX - ball.offsetWidth / 2 + 'px';
    ball.style.top = pageY - ball.offsetHeight / 2 + 'px';
  }

  function onMouseMove(event) {
    moveAt(event.pageX, event.pageY);
  }

  // (3) mousemove でボールを移動する
  document.addEventListener('mousemove', onMouseMove);

  // (4) ボールをドロップする。不要なハンドラを削除する
  ball.onmouseup = function() {
    document.removeEventListener('mousemove', onMouseMove);
    ball.onmouseup = null;
  };

};
```

<<<<<<< HEAD
コードを実行すると、何かおかしいことに気づきます。ドラッグ&ドロップの開始時に、ボールは "分岐" します: 我々はその "クローン" をドラッグし始めます。

=======
If we run the code, we can notice something strange. On the beginning of the drag'n'drop, the ball "forks": we start dragging its "clone".
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

```online
これは、アクションの例です:

[iframe src="ball" height=230]

マウスをドラッグ&ドロップし、奇妙な振る舞いをみてみてください。
```

ブラウザは、画像や自動的に実行する他の要素のための独自のドラッグ&ドロップを持っており、それが私たちのコードと競合するためです。

それを無効にするためには:

```js
ball.ondragstart = function() {
  return false;
};
```

これで、すべて大丈夫です。

```online
アクション:

[iframe src="ball2" height=230]
```

もう１つの重要な側面 -- 私たちは `ball` ではなく、`document` の `mousemove` を追跡しています。一見すると、マウスは常にボールの上にあり、その上に `mousemove` を置くことができるように見えるかもしれません。

しかし、覚えているように、`mousemove` は頻繁にトリガしますがピクセル毎ではありません。そのため、すばやく移動した後、カーソルはボールからドキュメント(またはウィンドウの外側)上のどこかにジャンプする可能性があります。

したがって、それをキャッチするために `document` でリッスンする必要があります。

## 正しいポジショニング 

上の例では、ボールは常にポインタの下で中央配置されています。:

```js
ball.style.left = pageX - ball.offsetWidth / 2 + 'px';
ball.style.top = pageY - ball.offsetHeight / 2 + 'px';
```

悪くはありませんが副作用があります。ドラッグ&ドロップを開始するために、私たちはボール上どこでも `mousedown` できます。もしボールの端でそれをした場合、ボールは突然中央になるために "ジャンプ" します。

ポインタに対する要素の初期のずれを維持するようが良いでしょう。

例えば、ボールの端でドラッグを開始する場合、ドラッグ中のカーソルは端のままであるべきです。

![](ball_shift.png)

1. 訪問者がボタン (`mousedown`) を押したとき -- 変数 `shiftX/shiftY` に、カーソルからボールの左上端の距離を覚えることができます。私たちはドラッグの間その距離を維持する必要があります。

    それらのシフト(ずれ)を取得するには、座標の減算をします:

    ```js
    // onmousedown
    let shiftX = event.clientX - ball.getBoundingClientRect().left;
    let shiftY = event.clientY - ball.getBoundingClientRect().top;
    ```

    JavaScript では、document に相対的な座標を取得するメソッドがないことに注意してください。そのため、ここではウィンドウに相対的な座標を使っています。

2. 次に、ドラッグの間はこのようにして、ポインタに相対的な同じシフトにボールを置きます。:

    ```js
    // onmousemove
    // ball has position:absoute
    ball.style.left = event.pageX - *!*shiftX*/!* + 'px';
    ball.style.top = event.pageY - *!*shiftY*/!* + 'px';
    ```

より良いポジショニングとなる最終的なコードです:

```js
ball.onmousedown = function(event) {

*!*
  let shiftX = event.clientX - ball.getBoundingClientRect().left;
  let shiftY = event.clientY - ball.getBoundingClientRect().top;
*/!*

  ball.style.position = 'absolute';
  ball.style.zIndex = 1000;
  document.body.append(ball);

  moveAt(event.pageX, event.pageY);

  // ボールを（pageX、pageY）座標の中心に置く
  function moveAt(pageX, pageY) {
    ball.style.left = pageX - *!*shiftX*/!* + 'px';
    ball.style.top = pageY - *!*shiftY*/!* + 'px';
  }

  function onMouseMove(event) {
    moveAt(event.pageX, event.pageY);
  }

  // (3) mousemove でボールを移動する
  document.addEventListener('mousemove', onMouseMove);

  // (4) ボールをドロップする。不要なハンドラを削除する
  ball.onmouseup = function() {
    document.removeEventListener('mousemove', onMouseMove);
    ball.onmouseup = null;
  };

};

ball.ondragstart = function() {
  return false;
};
```

```online
アクション (`<iframe>` の中):

[iframe src="ball3" height=230]
```

<<<<<<< HEAD
ボールの右下端でドラッグをする場合に、違いは特に顕著になります。以前の例ではボールはポイントの下に "ジャンプ" します。今は現在の位置からのなめらかにカーソルを追うことができます。
=======
The difference is especially noticeable if we drag the ball by its right-bottom corner. In the previous example the ball "jumps" under the pointer. Now it fluently follows the cursor from the current position.
>>>>>>> 30f1dc4e4ed9e93b891abd73f27da0a47c5bf613

## ドロップ可能を検出する 

前の例では、ボールは "どこにでも" ドロップすることができました。実際には、通常1つの要素を取り、別の要素へそれをドロップします。例えば、ファイルをフォルダに、またはユーザをゴミ箱に、などです。

抽象的には、私たちは "ドラッグ可能な" 要素を取り、"ドロップ可能な" 要素上にドロップします。

ドラッグ&ドロップの最後には、ドロップ可能なターゲットを知る必要があります -- 対応するアクションを行ったり、できれば、ドラッグ処理中にそれを強調表示したりします。

そのソリューションは興味深くもあり難解でもあるため、ここで説明しましょう。

最初のアイデアは何でしょう？恐らく潜在的なドロップ可能要素に `onmouseover/mouseup` ハンドラを設定し、マウスポインタがその上に現れたときに検出するやり方です。そうすると、その要素上でドラッグ/ドロップしていることが分かります。

しかし、これは動作しません。

問題は、私たちがドラッグしている間、ドラッグ可能な要素は常に他の要素の上にあることです。また、マウスイベントは最上位の要素でのみ発生し、下位の要素では発生しません。

例えば、以下は2つの `<div>` 要素があり、青の上に赤があります。この場合、赤は最上位であるため、青要素のイベントをキャッチする手段はありません。:

```html run autorun height=60
<style>
  div {
    width: 50px;
    height: 50px;
    position: absolute;
    top: 0;
  }
</style>
<div style="background:blue" onmouseover="alert('never works')"></div>
<div style="background:red" onmouseover="alert('over red!')"></div>
```

ドラッグ可能な要素も同じです。ボールは常に他の要素の上にあるため、そこでイベントが発生します。下位の要素でどんなハンドラを設定しても、それらは動作しません。

そういう訳で、ドロップ可能要素にハンドラを置くと言う最初のアイデアは実践では上手くいきません。それらは実行されないでしょう。

では、何をすればよいでしょう？

`document.elementFromPoint(clientX, clientY)` と言うメソッドがあります。これは指定された ウィンドウ相対座標上の最もネストされた要素を返します(座標がウィンドウの外の場合は `null` です)。

なので、任意のマウスイベントハンドラで、ポインタの下のドロップ可能要素を検出することができます。次のようになります:

```js
// マウスイベントハンドラの中
ball.hidden = true; // (*)
let elemBelow = document.elementFromPoint(event.clientX, event.clientY);
ball.hidden = false;
// elemBelow はボールの下の要素です. もしそれがドロップ可能であれば処理します
```

注意:`(*)` 呼び出しの前に、ボールを隠す必要があります。そうしなければ、ポインタ下の最上位の要素として、通常その座標にはボールがあるためです: `elemBelow=ball`

私たちはこのコードを使って、いつでも "飛んでいる場所" を確認することができます。そして、それが起きるとドロップを処理します。

"ドロップ可能な" 要素を探すよう拡張された `onMouseMove` のコードです:

```js
let currentDroppable = null; // 今飛んでいるドロップ可能要素

function onMouseMove(event) {
  moveAt(event.pageX, event.pageY);

  ball.hidden = true;
  let elemBelow = document.elementFromPoint(event.clientX, event.clientY);
  ball.hidden = false;

  // mousemove イベントはウィンドウ外をトリガする可能性があります(ボールが画面外にドラッグされたとき)
  // clientX/clientY がウィンドウ外の場合、elementfromPoint は null を返します
  if (!elemBelow) return;

  // 潜在的なドロップ可能領域は "droppable" クラスでラベル付されています (他のロジックの場合もあります)
  let droppableBelow = elemBelow.closest('.droppable');

  if (currentDroppable != droppableBelow) { // 変更がある場合
    // 私たちは飛んでいます(入ったか出たか)...
    // 注意: 両方の値は null になりえます。
    //   currentDroppable=null ドロップ可能領域にいなかった場合 (e.g 空白スペース)
    //   droppableBelow=null このイベント中、今ドロップ可能領域にいない場合

    if (currentDroppable) {
      // ドロップ可能領域を "飛び出る" 処理のためのロジック (強調表示の除去)
      leaveDroppable(currentDroppable);
    }
    currentDroppable = droppableBelow;
    if (currentDroppable) {
      // ドロップ可能領域に "入る" 処理のためのロジック
      enterDroppable(currentDroppable);
    }
  }
}
```

下の例では、ボールがサッカーゴールにドラッグされたとき、ゴールが強調表示されます。

[codetabs height=250 src="ball4"]

今、プロセス全体で、変数 `currentDroppable` の中に現在の "ドロップターゲット" があり、強調表示やその他のことをするのに使うことができます。

## Summary

We considered a basic `Drag'n'Drop` algorithm.

The key components:

1. Events flow: `ball.mousedown` -> `document.mousemove` -> `ball.mouseup` (cancel native `ondragstart`).
2. At the drag start -- remember the initial shift of the pointer relative to the element: `shiftX/shiftY` and keep it during the dragging.
3. Detect droppable elements under the pointer using `document.elementFromPoint`.

We can lay a lot on this foundation.

- On `mouseup` we can finalize the drop: change data, move elements around.
- We can highlight the elements we're flying over.
- We can limit dragging by a certain area or direction.
- We can use event delegation for `mousedown/up`. A large-area event handler that checks  `event.target` can manage Drag'n'Drop for hundreds of elements.
- And so on.

There are frameworks that build architecture over it: `DragZone`, `Droppable`, `Draggable` and other classes. Most of them do the similar stuff to described above, so it should be easy to understand them now. Or roll our own, because you already know how to handle the process, and it may be more flexible than to adapt something else.
