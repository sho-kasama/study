

## respond_toとは？

通常時ではHTML形式(いつでもウェブサイトで見る形)で結果を取得したいけど、明示的にJSON形式やXML形式を指定した場合はJSON形式やXML形式で返すようにするメソッドです。


### 例


`users_controller.rb`⬇️
```

class UsersController < Application
  def show 
    @user = { 'name' => 'Yamada', 'old' => '20' }
    
    respond_to do |format|
      format.html
      format.json { render :json => @user }
      format.xml  { render :xml => @user }
    end
  end
end

```


`app/views/users/show.html.erb`

```
<p>名前: <%= @user["name"] %]</p> 
<p>年齢: <%= @user["old"] %></p>
```

以上のファイルがあったとすると
`http://localhost:3000/users/show` へアクセスした時はHTML形式で結果が返ってきます。

```
名前: 山田
年齢: 20
```

<br>

次に、`http://localhost:3000/users/show.json`へアクセスした場合は、JSON形式で返ってきます

```
{
  name: "Yamada",
  old: "20"
}
```

<br>
<br>
`http://localhost:3000/users/show.xmlへアクセスした場合は`

```
this XML file dose not appear to have any style information
<hash>
  <name>Yamada</name>
  <old>20</old>
</hash>
```

以上のように、respond_toメソッドは、リクエストで指定されたフォーマット(HTML,JSON,XML)に合わせて結果を返すメソッドと覚えておけばいいかも


<br>

## 参考記事


<a href="https://teratail.com/questions/90663">respond_to do |format|とはどの様な事をするのでしょうか？細かい詳細をお聞きしたく・・</a>
