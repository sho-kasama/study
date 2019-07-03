

## メソッドのまとめ



### document.write(引数) 
write()の括弧の中に値を指定するとその値がブラウザに表示される。このメソッドの括弧の中に渡す値のことを引数と呼びます

上記のdocument.write()を使った文字列の出力をしましたが、document.write()はブラウザのレンダリングに悪影響を与えるということで、
HTML5では非推奨となっています。代替案としてgetElementById()メソッドとinnerHTMLプロパティを組み合わせて使う方法があります。

### getElementById()メソッドは、HTMLのID属性をしてしてHTML要素を取得します。
JavaScriptの中でもとても重要なメソッドと言えます。
getElementById()メソッドが返す値は要素のオブジェクトで、これを使って内容を変更することができます。

```
ex,
html
<div id="message">Smile : ) </div>

js
var mes = document.getElementById( "message" ) ; ⇦ IDを指定して要素を取得
console.log( mes ); ⇦ 取得結果をコンソールに出力
```


- addEventListener




### DOMContentLoaded

最初のHTMLドキュメントの読み込みと解析が完了した時に、スタイルシートや画像、サブフレームの読み込みと解析が完了した時にスタイルシートや画像、さぶフレームの読み込みが終わるのを
待たずに発火します。




