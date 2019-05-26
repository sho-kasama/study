## 参考記事

<a href="https://blog.ohgaki.net/stop-using-jsonp">JSONPは危険なので禁止</a><br>
<a href="https://qiita.com/nekoneko-wanwan/items/bedc0e826c0842ca0b11">はじめてajaxを使うときに知りたかったこと</a><br>
<a href="https://qiita.com/hisamura333/items/e3ea6ae549eb09b7efb9">初心者目線でAjaxの説明</a><br>
<a href="https://railsguides.jp/working_with_javascript_in_rails.html">Rails で JavaScript を使用する</a><br>
<a href="https://qiita.com/fezrestia/items/e669107a4a6e66618738">Rails 5.x標準で Ajax+(jQuery+Partial) でHTML部分更新する世界一シンプルなサンプル</a><br>
<a href="https://qiita.com/katsunory/items/9bf9ee49ee5c08bf2b3d">JavascriptのAjaxについての基本まとめ</a>




Ajaxまとめ


## 目次

0 同期と非同期とは
1. Ajaxとは
2. JSONとは
3. JSONPとは
4. 参考記事





## 0 同期と非同期とは 

#### 同期通信の場合
webブラウザからサーバーにリクエストを通信し、レスポンスが戻ってくる。<br>
この時に全ての情報を通信しているので一瞬画面が白くなる<br>
=>サーバーからレスポンスが返ってくるまで他の作業はできない

#### 非同期通信の場合
webブラウザから一部の情報をリクエストするので、
それ以外の部分は変わらない、なので面白がることはない。<br>
=>サーバーからレスポンスが返ってこなくても他の作業はできる<br>
一部の情報をサーバーに送信してそれを受け取り反映させる仕組みをAjaxという











## 1 Ajaxとは

Ajaxごは、Asynchronous JavaScript + XML の略称でJavaScriptを使って非同期でサーバーとやりとりをする通信のことです。<br>


* クライアントから非同期更新に必要なデータをサーバーに送る<br>
* サーバーはデータを受け取ってクライアントに整形済データを返す<br>
* クライアントはサーバから受け取った整形済データをDOMに反映する<br>


ざっくりこのような流れでAjaxは実現されてる。<br>
クライアントからデータを送ったり、サーバから整形済データが返ってきたと検知するところにJavascriptのXTR(XMLHttpRequest)という技術が使われていて、<br>
返って来たと検知するところにJavaScriptのXTR(XMLHttpRequest)という技術が使われていて、返ってくる整形済データがXMlだったりするので Asynchronous JavaScript + XML と呼ばれている。<br>
ただし、XMLは名前だけ残って良いて、デファクトスタンダートで返ってくるデータはJSONというフォーマットが多いい。

<br>
<br>

## JSONとは

`
json   # データ記法 
jsonp  # コールバック関数
`

JSONはJavaScript Object Notationの略で、<a href="http://pentan.info/doc/rfc/j4627.html">RFC4627が規定するデータ記述言語です</a><br>
その名が示す通り、JavaScriotの記法でデータを記述できる点が最大の特徴です。語法はJavaScriptですが、そのシンプルさから多くの言語がライブラリを用意しているためa<br>
プログラミング言語間でデータを受け渡せます。<br>


WebサービスではブラウザがJavaScriptを実行できるので相性が良いこと、XMLと比べてデータ表現の冗長性が低いことなどかの利点から<br>
Ajax通信に置けるデータフォーマットとして活用されます、



### メディアタイプ

JSONのメディアタイプは「application/json」です。<br>
以下のHTTPヘッダは、このメッセージのボディがUTF-8でエンコードしたJSONであることを意味します。
` Content-Type: application/json; charset=utf-8`

 XMLやHTMLと同様に特別な理由がない限りはUTF-8を使うのが無難です。
 

 
### データ型
 
 JSONに組み込みで用意されてるデータ型には次の6つがあります。<br>
 
 
 * オブジェクト
 * 配列
 * 数値
 * ブーリアン
 * null
 



#### オブジェクト
 
```
{
  "name": {
     "first": "Yohei",
     "last": "Yamamoto"
  },
  "blog": "http://yohei-y.blogspot.com",
  "age": 34,
  "interest": ["Web", "XML", "REST"]
}
```

オブジェクトは`{`で始まり、`}`で終わります<br>
メンバは`,`で区切り、メンバの名前と値は`:`で区切ります。<br>
この例は、name,blog,age,interestの4つのメンバをもつオブジェクトです<br>
メンバはそれぞれ順に、オブジェクト、文字列、数値、配列を値として持っています.



<br>

#### クロスドメイン通信の制限

JSONPを説明する前に、なぜJSONPが必要になるのかの背景をせつめい<br>

Ajaxで用いるXMLHttpRequest という JavaScriptのモジュールはセキュリティ上の制限からJavaScriptファイルを取得したのと同じサーバとしか通信できません<br>
JavaScriptが在るサーバとは別のサーバと通信できてしまうと、ブラウザで入力した情報をユーザが知らない間に不正なサーバに送信できてしまうからです。<br>
ちなみに、このように不特定多数のドメインに属するサーバにアクセスすることを「クロスドメイン通信」(ドメインをまたがった通信の意）と呼びます<br>
<br>
<br>
しかし、複数のドメインのサーバと通信できず、単一のドメインのみと通信をしなければならないのは大きな制限です。<br>
たとえば、自サービスでは地図データと郵便番号データを保持せずに、それらを提供している他のWeb API( Google map, ぐるなびのapiとか)から適宜取得することができないからです。<br>



##  3JSONPとは
<br>
JSONP (JSON with padding)とは、scriptタグを使用してクロスドメインな(異なるドメインに存在する)データを取得する仕組みのことである。<br>
HTMLのscriptタグ、JavaScript(関数),JSONを組み合わせて実現される。<br>
<br>
<br>


XHRだとサイト間をまたいでデータ共有できない制限を回避するために利用されてきた仕組みです。<br>
<br>


```
<script type='text/javascript'
src="http://another.domain.example.com/getjson?callback=parseResponse'>
```
このような感じでコールバックを指定して使います<br>

<script>タグでJSONを呼び出すとコールバック関数を使ってJSONデータを処理します。<br>
このコールバック関数を攻撃にすることにより、攻撃者は情報を不正に取得できます。<br>



