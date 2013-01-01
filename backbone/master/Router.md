---
title: Router.md
repository: backbone
branch: 'master'
layout: default
---

+  元文書: [backbone/index.html at 9890d49db164e63b9b56e9d664ec0aab2289e0de · documentcloud/backbone · GitHub](https://github.com/documentcloud/backbone/blob/9890d49db164e63b9b56e9d664ec0aab2289e0de/index.html "backbone/index.html at 9890d49db164e63b9b56e9d664ec0aab2289e0de · documentcloud/backbone · GitHub")

## Backbone.Router

多くの場合、Webアプリケーションはリンク可能、ブックマーク可能、シェア可能なURLをアプリ内での重要な所在地のために提供します。最近まで、これらの固定リンクを提供するためにハッシュフラグメント（`#page`）が使われていましたが、History APIの出現とともに、標準的なURL（`/page`）を使うことが可能になりました。 **Backbone.Router** はクライアントサイドページのルーティングのためのメソッド、それらを接続するアクションとイベントを提供します。History APIをサポートしていないブラウザでは、Routerは優雅なフォールバックとURLのフラグメントバージョンへの透過的な変換処理をおこないます。

ページのロード中に、アプリケーションがすべてのルーターの作成を完了した後、必ずルートの初期URLで`Backbone.history.start()`か`Backbone.history.start({pushState: true})`を呼び出してください。

### extend Backbone.Router.extend(properties, [classProperties]) 

カスタムルータークラスを作ることから始めます。特定のURLフラグメントにマッチした場合にトリガーされるアクションを定義し、ルートとアクションのペアの[routes](#Router-routes)ハッシュを提供してください。ルート定義の中で先頭のスラッシュの使用を避けるべきということに注意してください:

<pre class="javascript"><code>var Workspace = Backbone.Router.extend({

  routes: {
    &quot;help&quot;:                 &quot;help&quot;,    // #help
    &quot;search/:query&quot;:        &quot;search&quot;,  // #search/kiwis
    &quot;search/:query/p:page&quot;: &quot;search&quot;   // #search/kiwis/p7
  },

  help: function() {
    ...
  },

  search: function(query, page) {
    ...
  }

});
</code></pre>

### routes router.routes 

routesハッシュは[View](http://documentcloud.github.com/backbone/#View)の[eventsハッシュ](http://documentcloud.github.com/backbone/#View-delegateEvents)と似ており、ルーター上でURLとパラメーターを関数にマッピングします。ルートは、`:param`のようなスラッシュの間の単一のURL構成要素と一致するパラメーター部分や、`*splat`のような複数のURL構成要素に一致するsplat部分を含むことができます。

例えば、`"search/:query/p:page"`のルートは`#search/obama/p2`のフラグメントにマッチし，`"obama"`と`"2"`をアクションに渡します。`"file/*path"`のルートは`#file/nested/folder/file.txt`にマッチし、`"nested/folder/file.txt"`をアクションに渡します。

訪問者が戻るボタンを押すか、URLを入力して特定のルートがマッチした場合、アクションの名前の[イベント](http://documentcloud.github.com/backbone/#Events)が発火するので、その他のオブジェクトはrouterにlistenして通知を受けることができます。次の例では、`#help/uploading`を訪れたときに`route:help`イベントがrouterから発火します。

<pre class="javascript"><code>routes: {
  &quot;help/:page&quot;:         &quot;help&quot;,
  &quot;download/*path&quot;:     &quot;download&quot;,
  &quot;folder/:name&quot;:       &quot;openFolder&quot;,
  &quot;folder/:name-:mode&quot;: &quot;openFolder&quot;
}
router.on(&quot;route:help&quot;, function(page) {
  ...
});
</code></pre>

### constructor / initializenew Router([options]) 

新しいrouterをつくったときに、`routes`ハッシュを渡したいのであれば、オプションとしてそのまま渡すことができます。`initialize`関数が定義されていれば、全ての`options`が渡されます。

### route router.route(route, name, [callback]) 

手動でルーターのためのルートを作成し、`route`引数には[ルーティング文字列](http://documentcloud.github.com/backbone/#Router-routes)か正規表現を指定することができます。ルート文字列か正規表現からマッチしたそれぞれのキャプチャはコールバックの引数として渡されます。`name`引数はルートがマッチしたときに`route:name`イベントとしてトリガーされます。もし`callback`引数が省略された場合、`router[name]`が代わりに使用されます。

<pre class="javascript"><code>initialize: function(options) {

  // #page/10にマッチしたら&quot;10&quot;が渡される
  this.route(&quot;page/:number&quot;, &quot;page&quot;, function(number){ ... });

  // /117-a/b/c/openにマッチしたら&quot;117-a/b/c&quot;がthis.openに渡される
  this.route(/^(.*?)\/open$/, &quot;open&quot;);

},

open: function(id) { ... }
</code></pre>

### navigaterouter.navigate(fragment, [options]) 

URLを保存したいアプリケーション内の地点に到達したら、URLを更新するために **navigate** を呼び出します。route関数の呼びだしも行いたい場合は **trigger** オプションに`ture`を設定します。ブラウザの履歴にエントリを作成せずにURLを更新するためには **replace** オプションに`true`を設定します。

<pre class="javascript"><code>openPage: function(pageNumber) {
  this.document.pages.at(pageNumber).open();
  this.navigate(&quot;page/&quot; + pageNumber);
}

# Or ...

app.navigate(&quot;help/troubleshooting&quot;, {trigger: true});

# Or ...

app.navigate(&quot;help/troubleshooting&quot;, {trigger: true, replace: true});
</code></pre>

