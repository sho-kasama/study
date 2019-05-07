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
Action PackはMVC(Model-View-Controller)アーキテクチャにおけるV及びC(View-Controller)の機能に提供するRailsのコンポーネントです。<br>
Action PackはVとCにあたる機能を一度に提供しますが、コントローラーの機能はActionContorllerにまとめられており<br>
ビューの機能はAction Viewにまとめられています。
Action RecordはRailsにO/Rマッピング(ORM)の機能を提供するコンポーネントです。<br>
Action Recordを使うことでモデルのオブジェクトと関連付いたテーブルのレコードが対応付けられます。<br>
Action SupportはRailsを便利に様々なユーティリティクラスと標準ライブラリの拡張を集めたものです<br>
Active ResourceはRailsのアプリケーションから外部のRESTfulなAPIにアクセスする時の機能を提供するコンポーネントです。<br>











