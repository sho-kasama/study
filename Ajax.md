
Ajaxまとめ


## 目次


1. Ajaxとは
2. JSONとは
3. JSONPとは






. 同期と非同期とは 



## 1 Ajaxとは

Ajaxごは、Asynchronous JavaScript + XML の略称でJavaScriptを使って非同期でサーバーとやりとりをする通信のことです。<br>


* クライアントから非同期更新に必要なデータをサーバーに送る<br>
* サーバーはデータを受け取ってクライアントに整形済データを返す<br>
* クライアントはサーバから受け取った整形済データをDOMに反映する<br>
<br>
<br>

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

<br>
WebサービスではブラウザがJavaScriptを実行できるので相性が良いこと、XMLと比べてデータ表現の冗長性が低いことなどかの利点から<br>
Ajax通信に置けるデータフォーマットとして活用されます、

<br>
<br>


### メディアタイプ

JSONのメディアタイプは「application/json」です。<br>
以下のHTTPヘッダは、このメッセージのボディがUTF-8でエンコードしたJSONであることを意味します。
` Content-Type: application/json; charset=utf-8`

 XMLやHTMLと同様に特別な理由がない限りはUTF-8を使うのが無難です。
 
<br>
<br>
 
### データ型
 
 JSONに組み込みで用意されてるデータ型には次の6つがあります。<br>
 
 
 * オブジェクト
 * 配列
 * 数値
 * ブーリアン
 * null
 
<br>


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


## 3.JSONPとは
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
<br>



<a href="https://blog.ohgaki.net/stop-using-jsonp">JSONPは危険なので禁止</a>



### 3.クロスドメイン通信の制限

JSONPを説明する前に、なぜJSONPが必要になるのかの背景をせつめい<br>
Ajaxで用いるXMLHttpRequest という JavaScriptのモジュールはセキュリティ上の制限からJavaScriptファイルを取得したのと同じサーバとしか通信できません<br>
JavaScriptが在るサーバとは別のサーバと通信できてしまうと、ブラウザで入力した情報をユーザが知らない間に不正なサーバに送信できてしまうからです。<br>
ちなみに、このように不特定多数のドメインに属するサーバにアクセスすることを「クロスドメイン通信」(ドメインをまたがった通信の意）と呼びます<br>
<br>
<br>
しかし、複数のドメインのサーバと通信できず、単一のドメインのみと通信をしなければならないのは大きな制限です。<br>
たとえば、自サービスでは地図データと郵便番号データを保持せずに、それらを提供している他のWeb API( Google map, ぐるなびのapiとか)から適宜取得することができないからです。<br>


#### <script>要素による解決
 

XMLHttpRequestではクロスドメイン通信ができませんが、代替手段があります。<br>
HTMLの<script>要素を用いると、複数のサイトからJavaScriptファイルを読み込める<br>
 
 
 ```
  <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
      <script src="http://example.jp/map.js"></script>
      <script src="http://example.com/zip.js"></script>
      ...
    </head>
    ...
  </html>
 
 ```
<br>
<br>

上記の例では複数のドメイン（example.jpと example.com)からJavaScriptファイルを読み込んでいます。<br>
<script>要素は歴史的理由により通常はブラウザのセキュリティ制限を受けません<br>


