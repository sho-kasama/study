
# 目次

0. Rubyのライブラリ
1. RubyGemsとは <br>
1.1 Gemfileの-> という記号はどういう意味なのか <br>
2. Bundlerとは <be>
  2.1 Gemfile/Gemfile.lockとは <br>
  2.2 bundle install/bundle updateの違いとは<br>
3.

## 0. Rubyのライブラリ

Rubyのライブラリはgemという形式にまとめてrubygems.orgにて配布されるのが一般的です。<br>
gemには以下のような有用な情報が含まれます。<br>

・ メタデータ。名前、バージョン、説明、著者のメアドなど。 <br>
・ 含まれるファイルのリスト <br>
・ 実行ファイルとその場所のリスト (binなど) <br>
・ Rubyのload pathに含まれるべきパスのリスト(lib)など。 <br>
・ 必要となる他のライブラリ(依存関係) <br>

最後の「依存関係」というのがGemfileと重なるところ。<br>
Gemが依存関係を記述するときは、名前とバージョンを範囲をリストアップします。<br>
個々で重要なのは依存先ライブラリのソースについては気にしないということです。




## 1, RubyGemsとは
<br>
Rubyに関係するパッケージを総称してRubyGemsといいます。<br>
開発に便利なライブラリやフレームワークをパッケージにし、公開されたそれらはRubylist達は、RubyGems,Gem,Gemsと呼んでいます。<br>
Gemに限らずパッケージの依存関係を管理することが安定のためにも重要です。<br>





## 1.1 Gemfileの -> という記号はどういう意味なのか

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






<br>


## 2, Bundlerとは
Bundler の前にまず、Ruby に関係するパッケージを総称して RubyGems といいます。<br>
開発に便利なライブラリやフレームワークをパッケージして<br>
公開されたそれらを Rubyist 達は RubyGems、Gem、Gems と呼んでいます。<br>
Gem に限らずパッケージの依存関係を管理することが安定の為にも重要です。<br>
<br>
そして、Bundlerとは、それら依存関係を管理してくれるツールです。<br>
例えば、ある Gem が依存している別の Gem や、それらのバージョン管理であったり、他にも Test や Dev や Pro といった環境ごとに別のバージョンを使用する等に必要となります。<br>
このBundlerもRubyGems
`
gem install bundler
`

## 2.1 Gemfile/Gemfile.lock/gemspecとは

#### Gemfile
Gemの取得先を記述する<br>
通常はsourceとgemspecの2行、もしくはsourceの1行だけだいい<br>               


#### Gemfile.lockとは
開発環境と運用環境(production)とで同じでgemをインストールするために使います。<br>
`bundle`などで自動で生成されます。<br>
installしたgemのversionや取得先が記録される<br>
依存gemのバージョンと取得先が記録されます。<br>


#### gemspecとは

実際の情報を記述するファイル
```
Gem::Specification.new do |s|
  s.authors = []
  s.homepage = ''
・
・
・
```
gemの依存関係をgemの情報を記述するファイル
```
s.add_dependency '*****'
s.add_development_dependency '***'
```







## 参考記事


<a href="https://qiita.com/sumyapp/items/6843ceebbbfc09a2b6ac">Bundlerを使ったRubyGemsの依存関係管理</a> <br>
<a href="https://qiita.com/tsubasakat/items/169833d4c8baf79e1b52">Bundler, Gemfile, Gemfile.lock について</a> <br>
<a href="https://qiita.com/mochikichi321/items/ee0b7133524816f73e60">Bundlerを使ったGem管理について</a>  <br>
<a href="https://nishinatoshiharu.com/about-bundler/">意外とよくわかっていないbundlerについて</a> <br>
<a href="https://yu8mada.com/2018/04/22/what-does-tilde-greater-than-sign-mean-in-gemfile/">Gemfile の ~> という記号はどういう意味なのか</a> <br>
<a href="https://qiita.com/tnoda_/items/a04e761d595a742fcdca">gemspec と Gemfile と Gemfile.lock との違い．</a>
<a href="http://sanemat.github.io/archives/langturn.com-translations-33/">gemspecとGemfileの役割をはっきりさせておく</a>
