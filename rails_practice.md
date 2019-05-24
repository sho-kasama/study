## Ruby on rails の設計の問題


問題1 

```
class CommentsController < ActionController::Base
    def index
      respond_to do |format|
        format.rss
      end
    end
end
```
以下のコードの(A)に入れることで、CommentsControllerのindexアクションへ正常にアクセスできる選択肢を選択してください。

```
redirect_to (A)
```

#### 解説
redirect_toメソッドを使用することによって、Webサイトを表示しているブラウザは自動的に引数で指定した先へ遷移します。
選択肢のredirect_toメソッドの引数に指定しているメソッドは、Railsが名前付きルートを生成した時に自動で生成したヘルパーメソッドです。

CommentsControllerのindexアクションはrespond_toメソッドによって、RSSの形式のデータが欲しいとリクエストされた時にレスポンスを返すように設定されています。他のデータの形式は指定されていないので、リクエストで別の形式の要求があってもエラーが発生します。
そのため、"/comments.rss"というパスを生成するヘルパーメソッドが正解です。名前付きルートに対応するヘルパーメソッドは、"formatted_"という文字がメソッド名の前に付くと、引数にデータの形式を指定できます。
そして、RAILS_ROOT/config/routes.rbで"map.resources"と設定した場合、名前付きルートと対応付けられたヘルパーメソッドが自動で生成されます。indexアクションへのパスを返すヘルパーメソッドは、モデル名の複数形と"_path"というメソッド名になります。
上記の"formatted_"の指定と合わせることで、正解は"fomatted_comments_path"になります。




## 問題2
Railsの規約に従ったREST的なWebサービスが「http://books.example.com」というURIで提供されているとします。次のプログラムは、<br>
このWebサービスのリソースをRailsアプリケーション内で通常のモデルと同じように扱っています。(A)に入る正しい選択肢を選んでください。


```
class Book < (A)
  self.site = 'http://books.example.com'
end
 
# Use case
books = Book.find(:all)
Book.create(:title => "foo", :price => 450)
```



#### 解説
Railsでは、Railsの規約に従ったREST的なWebサービスを、ActiveRecordによるモデルと類似したインターフェイスで扱えるようにするためのコンポーネントとして、ActiveResourceが用意されています。<br>
通常のActiveRecordによるモデルでは、CRUD操作の結果として、モデルに関連付いたDB上のテーブルを操作しますが、ActiveResourceを継承するクラスでは、DBの代わりにWebサービスに対して同じようにCRUD操作を行うことができます。<br>
ActiveResourceを利用することによって、上記のようなWebサービスを、統一的な操作方法でRailsアプリケーション自身のモデルのように扱えるメリットがあります。<br>
以上のことから、本問題の正解は(A)となります。<br>



## 問題3
config/routes.rbのルーティングを以下のように設定しました。
```
map.resources :articles
```


createアクションへアクセスするのに正しいパスとHTTPメソッドの組み合わせを以下の選択肢の中から選択してください。

#### 正解
(c) http://localhost:3000/articles, POST

#### 解説
```
map.resources :articles
```

RAILS_ROOT/config/routes.rbに上記の設定をおこなうことによって、RailsのアプリケーションはArticlesControllerの特定のアクションに対するルートを作成します。<br>
作成されるルートは、データベースにCRUD(Create, Read,Update, Destroy)な操作をおこなうアクションに対するルートです。<br>
他のHTMLメソッドと違って、createアクションはパスに対して、/idや/newなどの指定がつかない<br>



<br>
<br>

## 問題4
MVC(Model-View-Controller)アーキテクチャのViewとControllerの役割を担うRailsのコンポーネントとして正しいものは？


#### 解説
`Action Pack`はMVC(Model-View-Controller)アーキテクチャにおけるV及びC(View-Controller)の機能に提供するRailsのコンポーネントです。<br>
`Action Pack`はVとCにあたる機能を一度に提供しますが、コントローラーの機能はActionContorllerにまとめられており<br>
ビューの機能は`Action View`にまとめられています。
`Action Record`はRailsにO/Rマッピング(ORM)の機能を提供するコンポーネントです。<br>
`Action Record`を使うことでモデルのオブジェクトと関連付いたテーブルのレコードが対応付けられます。<br>
`Action Support`はRailsを便利に様々なユーティリティクラスと標準ライブラリの拡張を集めたものです<br>
`Active Resource`はRailsのアプリケーションから外部のRESTfulなAPIにアクセスする時の機能を提供するコンポーネントです。<br>


<br>



## 問題5

Railsで想定されるモデルのクラス名とデータベースのテーブル名の関係を表す組み合わせとして、正しいものを選んでください。

#### 解説
Railsで想定されるモデルのクラス名は先頭の文字が大文字で、続いての先頭文字意外の文字は小文字である「Calendar」のような単語から構成されたものです<br>
複数の単語をクラス名に盛り込むのに、単に「HolidayCalendar」のように繋いで複合語として書きます。<br>
この書き方はキャメルケースとも言います。<br>
<br>
Railsで想定されるテーブル名はすべて小文字で書き、複合語はアンダースコア()で繋いでholidaycalendarsのように構成します。<br>
因みに、このことは“アンダースコア化”といいます。<br>


<br>

## 問題6

Railsのデフォルトのルーティング設定を前提とした上で、以下のコントローラ名、アクション名とidパラメータに解釈されるURLを選んでください。

```
コントローラ名: CalendarsController
アクション名: reset
idパラメータ: 1
```

#### 解説
Railsアプリケーションでは、クライアントがリクエストしたURLに対して、なんのコントローラーとアクションが呼び出されるかを決定する仕組みとしてルーティングがある。<br>
ルーティングのデフォルト設定ではリクエストのURLは次のように解釈される

```
コントローラ名/アクション名/ID
```

三番目の要素はアクションの対象となるリソースのIDとしてpramsハッシュの:idキーとして設定されます。<br>
このIDはDBのレコードのIDを指します。<br>


<br>
<br>

## 問題7
以下のコードがエラーにならずに「Greetings, Eartling!]を出力して正常終了するように、選択肢を選ぶ。

```
def greeting
  puts "Greetings, #{ (A) }!"
end
greeting { "Earthling" }
```

## 解説
Rubyのメソッドにはブロックを与えることができる<br>
メソッドの定義の中にyieldを使うことによって、与えられたブロックに対してパラメーターをつけて呼び出すことができる<br>
メソッドの中のyieldの引数は、ブロック側ではブロックの冒頭に定義してあるブロックパラメーターとして受け取ることができます<br>
そして、ブロックが返す戻り値は、メソッド側ではyieldメソッドの戻り値として受け取ることができる問題文のコードの（A)としてyieldを使うことにすると、ブロックの戻り値「"Earthling"」が式展開によって#{ yield }の代わりに挿入されます。


## 問題8

以下のコードを実行した時の動作として正しい選択肢を選んでください。

```
 def yielder(input)
   yield input
 end
puts yielder("Ruby dreams")
```

## 解説
Rubyのメソッドにはブロックを与えることができます<br>
メソッドの定義の中にyieldを使うことによって、渡されたブロックに対してパラメーターをつけて呼び出すことができます<br>
しかし、yield式を含むメソッドの呼び出しにはブロックが期待されます<br>
ブロックが指定されていない呼び出しはLocalJumpErrorになります。<br>
コードを最後の行のように置き換えると処理が正常終了します

```
puts yielder("Ruby dreams") { true }
```

<br>
<br>

## 問題9

以下のコードを実行した時に正しい選択肢を選ぶ

```
class Book
  def initialize(args)
    @title  = args[:title]
    @author = args[:author]
    @year   = args[:year]
  end
end
book = Book.new({:title => "Ruby and friends"}, {:year => 1996})
```

## 解説
問題文の「initilize」メソッドは、「args」引数をHashクラスのインスタンスとして受け取るように定義してあります。<br>
問題のコードは最後の行で新しいBookクラスのインスタンスを作っています<br>

```
book = Book.new({:name => "Ruby and friends"}, {:year => 1996})
```

Bookクラスの「initilize」メソッドは一つだけの引数を受け取ることができます。<br>
「initialize」メソッドの中の処理は引数「args」に格納されるハッシュの中から３つの値を取り出して、それぞれ３つのインスタンス変数に代入します。<br>













