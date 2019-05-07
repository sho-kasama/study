

## RubyGemsとは
Rubyに関係するパッケージを総称してRubyGemsといいます。<br>
開発に便利なライブラリやフレームワークをパッケージにし、公開されたそれらはRubylist達は、RubyGems,Gem,Gemsと呼んでいます。<br>
Gemに限らずパッケージの依存関係を管理することが安定のためにも重要です。<br>






## Bundlerとは










## Gemfileの -> という記号はどういう意味なのか

RubyGemsの依存関係を管理してくれるBundlerのGemfile内で使われる`~>`という記号はどういう意味なのでしょうか。<br>
Bundler のバージョンは 1.16.1 になります。<br>
例えば次のようなGemfileがあった場合は <br>
```
source 'https://rubygems.org'
gem `nokogiri`
gem 'rack', '~> 2.0.1`
gem 'rspec'
```

次の行には`~>`が使われています

```
gem 'rack', '~> 2.0.1`
```
もしその記号が `~>` ではなく`>`であれば`2.0.1`より大きいバージョンを,`>=`であれば`2.0.1`以上のバージョンを指定することになりますが`~>`は一体どのようなバージョンを指定することになるのでしょうか.<br>


答えは`2.0.1`以上`2.1.0`未満のバージョンを指定することになります<br>


なので次のように書き換えることもできます<br>

```
gem 'rack', '>= 2.0.1', '< 2.1.0'
```

もう一つの例として, 次のような場合<br>


```
gem 'nokogiri', '~> 1.4.2'
```

このように書き換えられます<br>

```
gem 'nokogiri', '>= 1.4.2', '< 1.5.0'
```

Gemfile で ~> という記号をを見かけたときはそう言う意味になります<br>





## 参考記事


<a href="https://qiita.com/sumyapp/items/6843ceebbbfc09a2b6ac">Bundlerを使ったRubyGemsの依存関係管理</a> <br>
<a href="https://qiita.com/tsubasakat/items/169833d4c8baf79e1b52">Bundler, Gemfile, Gemfile.lock について</a> <br>
<a href="https://qiita.com/mochikichi321/items/ee0b7133524816f73e60">Bundlerを使ったGem管理について</a>  <br>
<a href="https://nishinatoshiharu.com/about-bundler/">意外とよくわかっていないbundlerについて</a> <br>
<a href="https://yu8mada.com/2018/04/22/what-does-tilde-greater-than-sign-mean-in-gemfile/">Gemfile の ~> という記号はどういう意味なのか</a> <br>
<a href=""></a>
<a href=""></a>
