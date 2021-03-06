

## 基本的な使い方

- [ ] <a href="https://jp.vuejs.org/v2/guide/instance.html">はじめに</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/instance.html">Vue インスタンス</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/syntax.html">テンプレート構文</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/computed.html">算出プロパティとウォッチャ</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/class-and-style.html">クラスとスタイルのバインディング</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/conditional.html">条件付きレンダリング</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/list.html">リストレンダリング</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/events.html">イベントハンドリング</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/forms.html">フォーム入力バインディング</a>
- [ ] <a href="https://jp.vuejs.org/v2/guide/components.html">コンポーネントの基本</a>


- [ ] <a href="https://jp.vuejs.org/v2/api/#%E3%82%AA%E3%83%97%E3%82%B7%E3%83%A7%E3%83%B3-%E3%83%87%E3%83%BC%E3%82%BF">Vue api (用語集) </a>


## 基礎から学ぶVue.js

- [ ] <a href="https://cr-vue.mio3io.com/tutorials/todo.html#%E5%AE%8C%E6%88%90%E5%BD%A2">基礎から学ぶVue.js</a>


## Vuexとは？



- [ ] <a href="https://qiita.com/terraphic/items/078dfbadcd75ad336ed4">Vuexで状態管理の大事さを知る</a>
- [ ] <a href="https://vuex.vuejs.org/ja/">Vuex とは何か？</a>





#### Vue.jsとは？

ユーザーインターフェイスを構築するためのプログレッシブフレームワークです。
中核となるライブラリはview層だけに焦点を当てています。
Vueは要素がVueによって挿入/更新/削除された時、自動的にトランジションエフェクトを適用できる強力なトランジション効果システムも提供します。

<br>

#### データバインディング構文とは？

Vue.jsはDOMベースのテンプレートの実装を使用しています。これは全てのVue.jsテンプレートは本質的に
有効になり、特別な属性で拡張されたHTMLを解析可能になるということを意味します。
また、Vueのテンプレートは本質的に文字列ベースのテンプレートとは異なるということを忘れないでください。

<br>

#### インスタンスライフルサイクルフック

名Vueインスタンスは、生成時に一連の初期化を行います。
例えば、データーの監視のセットアップやテンプレートのコンパイル、DOMへのインスタンスのマウント、データが変化したときの DOM の更新などがあります。その初期化の過程で、特定の段階でユーザー自身のコードを追加する、いくつかの ライフサイクルフック(lifecycle hooks) と呼ばれる関数を実行します。


ライフサイクルの様々な段階で呼ばれるフックがあります。`mounted`,`updated`などがあります。<br>
全てのライフサイクルフックは、`this`がVueインスタンスを指す形で実行されます。

<br>


#### ディレクティブ

ディレクティブは`v-`から始まる特別な属性です。ディレクティブ属性値は、単一のJavaScript式を期待します。(ただし、`v-for`は例外でこれに付いては後から説明します。)ディレクティブの仕事は、属性値の式が変化したときに、リアクティブに副作用を DOM に適用することです。


<br>

#### 省略記法

`v-bind`と`v-on`に対しては特別な省略記法を提供します。

```
<!--　完全な構文 -->
<a v-bind:href="url">....</a>

<!-- 省略記法 -->
<a :href="url">...</a>

<!-- 動的引数の省略記法 (2.6.0 以降 ) -->
<a :[key]="url">...</a>
```

```

<!-- 完全な構文 -->
<a v-on:click="doSomething"> ... </a>

<!-- 省略記法 -->
<a @click="doSomething"> ... </a>

<!-- 動的引数の省略記法 (2.6.0 以降) -->
<a @[event]="doSomething"> ... </a>

```


`:`や`@`は属性名に利用可能な文字です。


<br>

#### 算出プロパティvsメソッド

算出プロパティとメソッドのアプローチは同じ結果になります。
しかしながら、算出プロパティはリアクティブな依存関係にもとづきキャッシュされるという違いがあります。
キャッシングしたくない場合は、メソッドを使いましょう。

<br>

#### 算出プロパティvs監視プロパティ

VueはVueインスタンス上のデータの変更を監視し反応させることができる。
より凡用的な監視プロパティ(watched property) を提供しています。<br>
watcgコールバックよりも、多くの場合は算出プロパティを利用する方が綺麗なコードがかけます。

<br>

#### ウォッチャ

多くの場合では算出プロパティの方が適切ではありますが、カスタムウォッチャが必要な時もあるでしょう。データの変更に対して反応する、より汎用的な watch オプションを Vue が提供しているのはそのためです。データが変わるのに応じて非同期やコストの高い処理を実行したいときに最も便利です。

「ウォッチャ」とは、特定のデータまたは算出プロパティの状態を監視して、変化があったとき登録した処理を自動的に実行します。つまり、データの変化をトリガにしたフックです。

#### ウォッチャの使い方

コンポーネントの```watch```オプションに、監視するデータの名前と変化したときに呼び出されるハンドラを定義します。もし、比較が必要なら、第一引数として「新しい値」と、第二引数として「古い値」を受け取れます。

```
new Vue({

  watch: {
    監視するデータ: function(新しい値、古い値) {
      // valueが変化したときに行いたい処理
    },
    'item.value': function(newVal, oldVal) {
      // オブジェクトのプロパティも監視できる
    }
   }
})
```

#### keyの役割

キーを指定している場合と指定していない場合では、リストに対して操作をしたとき次のような違いが起きます。


写真


`key=1`というように文字列を指定することもできますが、繰り返しの中では全て同じ「１」になってしまい。これでは意味を成しません。<br>
その為、要素内のユニークなIDである`id`プロパティをキーとしてデータバインディングする必要があるのです。

* 不変でユニークなキーを設定する

要素の削除や並び替えも考慮して「不変でユニークなキー」を設定しましょう。
例えば、配列のインデックスはユニークですが、要素を削除したりシャッフルすれば変わってしまうのでデータに対して不変ではありません。<br>
また。別の`v-for`だとしても同じ親要素内で重複はできません。




<br>

## 用語集


#### el
Connect to DOM


#### data
Store Data to be used

#### methods
Methods of this Vue Instance

#### computed 
Dependent Properties



#### {{ }}
  
{{ }}でVueインスタンスの要素を呼び出すことができる。  

#### `new Vue`
Webアプリケーションは、`new Vue`で作成されたルートVueインスタンス(root Vue instance)で構成され、必要に応じてネストされたツリーや再利用可能なコンポーネントで形成されます。

  
#### `v-bind`

HTML要素をVue.jsで動的に指定したい場合は```v-bind```を使います。



#### `v-for`

```
<li v-for="各要素を代入する変数名 in 繰り返したい配列やオブジェクト>
```       
           

#### `v-once`

`v-once`ディレクティブは初回だけテンプレートを評価しそれ以降は静的なコンテンツとして扱います。
描画された後に`message`プロパティが変わってもDOMは更新されません。

```
<a v-bind:href="url" v-once>
  Hello {{ message }}
</a>
```

  
#### `v-html`

マスタッシュ構文では全てプレーンテキストとして扱われる為、HTMLとして表示したい場合はv-htmlディレクティブを使用します。
`v-html`はHTMLタグのまま出力するときに用います。
Mustacheを使った描画では、XSS対策のため、必ずHTMLエンティティ化されます。<br>
HTMLタグをそのまま表示させたい場合は`v-html`ディレクティブを使用します。主にAPIから取得したHTML文章を描画するときに使用します。主にAPIから取得したHTML文章を描画するときに使用します。

JavaScript

```
new Vue({
  el: '#app',
  data: {
    message: 'Hello <strong> Vue.js</strong>'
  }
})
```

html
```
<span v-html="message"></span>
```

## v-htmlテンプレートを信頼できるコンテンツに

XSS脆弱性を引き起こす為`v-html`ディレクティブを使用するデータ、テンプレートは信頼できるコンテンツのみを使用する。
例えば。データーベースに保管されたユーザー情報やコメントやURLから受け取ったパラメーターやクエリといった、ユーザーから提供された情報をそのまま使用しないようにする。z




#### `v-on`
イベントリスニングします。


#### `v-text`

要素内のテキストコンテンツが単一のMustacheのみで構成される場合、代わりに`v-text`ディレクティブを使って同じようにテキストコンテンツをバインドできます。


JavaScript
```
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js'
  }
})
```

mustacheの代わりにtextを使用

```
<span v-text="message"></span>
```
  

#### `v-if`
はディレクティブなので、単一の要素に付加する必要があります。



#### `v-show`
条件的に要素を表示するための別のオプションです。`v-show`による要素は常に描画されてDOMに維持するということです。


#### v-ifとv-showの違いと使い分け方

`v-if`と`v-show`を使用するときの条件の書き方は同じですが、描画結果を見るとおり動作に大きな違いがあります。<br>


<a href="https://qiita.com/r_chiba/items/15440197733e3e8bc7b1">参考記事</a>
![v-show](https://github.com/sho-kasama/study/blob/master/img/v-show%E3%81%A8v-bind.png)


* v-if条件による描画
条件を満たさなかった場合、要素はDOMレベルで削除され全ての監視は解除されます。
コンポーネントならインスタンスは破棄され、次に描画されるときには状態は初期化されてます。
内側にディレクティブやコンポーネントを多用していたり、特定のデータを持っていないとエラーが起きる場合には`v-if`を使用するといいでしょう。

* v-show条件による表示
条件を満たさなかった場合、単純に`display:none;`スタイルを付与します。目に見えなくても、内側は常にリアクティブで監視されていることに注意しましょう。
内側にディレクティブやコンポーネントが少なく、切り替えの頻度が高いものは`v-show`を使用するとパフォーマンスがよくなります。




#### `v-model`
`v-model`を使えば,Vueインスタンスの`data`をHTML要素にバインドできます。<br>
変更された場合は、その値を参照しているDOM全てに反映されます。



#### `v-pre`

`v-pre`ディレクティブは、子コンポーネントを含む内側のHTMLのコンパイルをスキップして、情的なコンテンツとして扱います。<br>
サーバーサイドレンダリング時のXSS対策に用いたり、操作をする予定のない長いHTML文書を記述しているときに使用すると、パフォーマンスの向上に繋がります。<br>


```
<a v-bind:href="url" v-pre>
  Hello {{ message }}
</a>
```



#### @

`v-on:`の省略記法で、`@click="link"`のようにかけます。
また、`v-bind`の代わりに`:`も使えます。


#### computed

Vueインスタンスの`comouted`オブジェクトは、`methods`に似ていますが、dataプロパティのように処理結果を保持させるときに使います。<br>
`methods`と違い、呼び出すときに`()`は不要です。


<br>

#### watch

Vueインスタンスの`watch`オブジェクトは、特定のプロパティの変化をトリガーに処理を走らせるときに使います。<br>
`data`だけでなく`compited`のプロパティも`watch`できます。


<br>


#### `v-if`vs`v-show`

<br>

`v-if`はイベントリスナと子コンポーネント内部の条件ブロックが適切に破棄され、そして切り替えられるまでの間再作成される"リアル"な条件レンダリングです。
`v-if`は遅延描画です。初期表示に置いてfalseの場合、何もしません。条件付きブロックは、条件が最初にtrueにされるまで描画されません。一方で、`v-show`はとてもシンプルで、要素は初期状態に関わらず常に描画され、シンプルなCSSベースの切り替えとして保存されます。
とても頻繁に何かを切り替える必要があれば `v-show`
条件が実行時に変更することがほとんどない場合は`v-if`

<br>


## JSフック

transitionで使えるJSフックは次の通りです。

- before-enter
- enter(done必要)
- after-enter
- after-enter-cancelled
- before-leave
- leave(done必要)
- after-leave
- after-leave-cancelled


## イベント修飾子



#### .stop

event.stopPropagation()を呼ぶ

```
<div @click="handler('親')>
  <div @click.stop="handler('子')">
    ボタン
  </div>
</div>

```
通常同じイベントをハンドルした、DOMがネストされている場合、親要素に向かってイベントが連鎖する。<br>
.stopをつけるとhandler('子')は実行されるが、handler('親')は実行されない。


<br>


#### .prevent

event.preventDefault()を呼ぶ

```
<a href="#top" @click.prevent="handler"></a>
```

handlerは実行されるが,#topに移動はしない。

#### .capture

キャプチャモードでDOMイベントをハンドルする。<br>
つまりルート要素から順番にイベントが実行される。

```
<div @click="handler('親')">
  <div @click.stop="handler('子')">
    ボタン
  </div>
</div>
```
handler('親') -> handler('子')の順番で実行される。

イベントが発生すると、キャプチャフェーズでルート要素から要素を探し、ターゲットフェーズでイベントハンドラ実行、バブリングフェーズでルートまで要素を遡ります。<br>
通常はターゲットフェーズでイベントハンドラを実行しますが、キャプチャモードにするとキャプチャフェーズでイベントが発生します。<br>


![event](https://github.com/sho-kasama/study/blob/master/img/event_phase.png)


#### .self

event.targetが自分自身の場合のみハンドラが呼び出される
(こ要素は呼び出されない)

```
<div v-on:click.self="handler">ボタン</div>
```

#### .once
最大一回ハンドラを呼び出す。

#### .passive
event.preventDefault()を呼び出さないことを明示
(.preventとの併用不可)

#### .enter
キー修飾子。エンターボタンを押した場合にハンドラを呼び出す。



## ライフサイクル


![ライフサイクル.1](https://github.com/sho-kasama/study/blob/master/img/%E3%83%A9%E3%82%A4%E3%83%95%E3%82%B5%E3%82%A4%E3%82%AF%E3%83%AB.1.jpg)
![2](https://github.com/sho-kasama/study/blob/master/img/%E3%83%A9%E3%82%A4%E3%83%95%E3%82%B5%E3%82%A4%E3%82%AF%E3%83%AB.2.jpg)



#### ライフサイクル,参考記事

- [ ] <a href="https://qiita.com/chan_kaku/items/7f3233053b0e209ef355">Vueのライフサイクルを完全に理解した</a>
- [ ] <a href="https://qiita.com/htkzhtm/items/ab4bb687f47c74b4e4ec">Vueのライフサイクル</a>


## what's export degault?

export文は指定したファイル(またはモジュール)から関数、オブジェクト、プリミティブをエクスポートするために使用する。<br>

importする際に指定がなければそのクラスや関数を呼ぶもの、importする際にfefualt以外のクラスや関数を呼び出したいときは、
{}でクラスやファイル名を指定して呼び出すことができる






## 参考記事


- [ ] <a href="https://qiita.com/hosomichi/items/49500fea5fdf43f59c58#%E3%82%A4%E3%83%99%E3%83%B3%E3%83%88%E3%83%95%E3%82%A7%E3%83%BC%E3%82%BA%E3%81%A8%E3%81%AF">DOMイベントのキャプチャ/バブリングを整理する 〜 JSおくのほそ道 #017</a>
- [ ] <a href="https://qiita.com/Yorinton/items/f7eb54f05609750da7f5">[メモ]Vue.jsイベント修飾子一覧</a>
- [ ] <a href="https://qiita.com/seya/items/93a0055c8fdab62d584f">コンポーネントの書き方</a>
- [ ] <a href="https://qiita.com/seya/items/794b25cfc0cf8ac10f1b">勉強になる海外の動画サイト</a>
- [ ] <a href="https://qiita.com/kimullaa/items/2bf8948dffb8c52d2b6b">Vuejs APIアクセスはcreatedとmountedのどちらで行う？</a>
- [ ] <a href="https://ginpen.com/2016/12/06/vue-computed/">computedすごいぞ賢いぞ！</a>
- [ ] <a href="https://qiita.com/fumix/items/9c8da630de8176669955#%E3%82%A4%E3%83%B3%E3%82%AF%E3%83%AA%E3%83%A1%E3%83%B3%E3%82%BF%E3%83%AB%E3%82%B5%E3%83%BC%E3%83%81">Vue.jsでなにか作ってみたときに参考にしたサイトとかのリンク集</a>
- [ ] <a href="https://qiita.com/kaorina/items/bb261a119b9f02e02c2d">Vue.jsの便利な機能coumptedとは？</a>

