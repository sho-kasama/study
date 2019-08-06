

## 単位まとめ



## Viewport パーセンテージ

vwのViewportのイニシャルで、それぞれこのような意味を持っています。

vm viewport width ビューポートの幅に対する割合<br>
vh viewport height ビューポートの高さに対する割合<br>
vmin viewport minimum ビューポートの幅と高さのうち、値が小さい方向に対する割合<br>
vmax viewport max ビューポートの幅と高さのうち、値が大きい方に対する割合<br>



## %と何が違うのか？

画像の幅をビューポートの幅に対する割合で指定するのであれば、確かに`%`で事足りるが、
%の場合は対象となる要素のプロパティが親要素のそれと紐付けられるため、必ずしもビューポートの幅が基準になるとは限りません。もし画像が div といったコンテナ要素の中にあれば、そのコンテナ要素の幅に対する割合で計算されます。

<br>

さらに`width`は必ず親要素のwidthに対する割合で計算され、`height`は親要素のheightに対する割合で計算されます。

<br>
`vw`,`vh`にはそのようなプロパティの紐付けがありません。以下のように記述すれば、画像の幅をビューポートの高さを元にした長さに指定することができます。

`
img {
  display: inline-block;
  margin: auto;
  width: 10vh;  /* ビューポートが 600pxだとしたら、画像の幅は60pxになる */
}

`


## 参考記事

- [ ] <a href="https://dev.classmethod.jp/ria/html5/css-length-viewport/">CSS には vw, vh, vmin, vmax という単位がある</a>






