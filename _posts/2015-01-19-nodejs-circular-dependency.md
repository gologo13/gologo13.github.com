---
id: 929
title: node.jsにおけるcircular dependency問題に対処するための3つの方法
date: 2015-01-19T00:40:09+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=929
permalink: /2015/01/19/nodejs-circular-dependency/
s4_url2s:
  - 
s4_image2s:
  - 
s4_ctitle:
  - 
s4_cdes:
  - 
categories:
  - javascript
  - node.js
---
node.js でコードを書いている時にハマった **circular dependency** という問題とその対処法について紹介します。

## circular dependency

この問題は **cyclic dependency** とも呼ばれ、日本語だと **循環参照** とか **循環依存関係**と呼びます。これはどういう問題かというと、**あるファイルを require したときにその結果が空のオブジェクトとして返される問題** です。 この問題に直面した時はなんでこうなるのか全く理解できなかったのですが、よくよくコードを見てみると、あるファイルとあるファイルがお互いにrequireし合っていることに気づき、色々調べてみるとこういう問題があることがわかりました。

以下にこの問題を再現させるサンプルコードを示します。



これらのコードを見ると、main.jsがa.jsを、a.jsがb.jsを、b.jsがa.jsをそれぞれrequireしていますね。 main.js を実行してみると、以下のように実行エラーになります。cyclic dependency のため A というオブジェクトが空オブジェクトになっています。空なので、getId というキーでアクセスしても undefined が返っています。

<pre class="lang:shell">$ node main.js
/Users/yohei/circularDependency/example/b.js:8
console.log('I got the id: ', A.getId());
^
TypeError: undefined is not a function
at Object.stuff (/Users/yohei/circularDependency/example/b.js:8:39)
at Object.doStuff (/Users/yohei/circularDependency/example/a.js:16:17)
at Object.&lt;anonymous> (/Users/yohei/circularDependency/example/main.js:4:14)
...
at node.js:809:3
</pre>

この問題は、**モジュールAが読み込まれる前にそのモジュール自身が読み込まれた時**に発生します。

上のサンプルコードの require の流れに着目してみましょう。

main.js（2行目）var A = require(&#8216;./a&#8217;);
  
→→a.js（3行目）var B = require(&#8216;./b&#8217;);
  
→→→→b.js（３行目）var A = require(&#8216;./a&#8217;);
  
→→→→b.js 読み込み完了
  
→→a.js 読み込み完了

流れを見てわかるように、a.js の読み込みが完了する前に b.js の中で a.js が読み込まれています。a.js の読み込みは完了していないので、b.js の３行目では空のオブジェクトが返っています。

### ではどうすべきか

この問題はかなりデバッグしづらいです。できれば事前にみつけたいですね。この問題を事前に見つけるためには、**CIで自動テストを継続的に実行させることが重要**ですね。ソースコードを眺めていてもこの問題を見つけるのが難しいためです。

こういう問題が起こること自体、ある意味モジュール化の仕方に問題があるとも言えるのですが、がっつり設計し直すことも難しい状況もあると思うので、 大きく構造を変えずにこの問題を解決させる方法について紹介してみます。方法の名前は勝手に命名していますｗ

### 方法1：module.exports first

require(&#8216;./b&#8217;) する前に module.exports を書く方法です。

オリジナルのa.jsと上のコードを比べてみると、真っ先にmodule.exportsにオブジェクトを代入しています。requireよりも先にモジュールAをexportすることで、circluar dependencyを回避しています。

この方法でコードを書き換える場合、コーディングスタイルによっては上の例のように大幅なファイル変更が必要になる場合があります。ちなみに、**普段からmodule.exports firstでコードを書く癖をつけておく**と、circluar dependencyの問題にハマる可能性もグッと下がるのでオススメです。

### 方法2：lazy require

利用したいモジュールを先頭で require するのではなく、必要なときに初めてrequireする方法です。

この方法は最も既存のコードへの影響が少ない方法です。 このファイルがrequireされるときに、init関数自体は実行されないので、cyclic dependency は回避出来ています。init関数が呼ばれて初めて、b.jsが読み込まれます。

関数呼び出しのたびに、requireされるのでオーバーヘッドが若干気になりますが、 [requireされた結果はキャッシュされる](http://nodejs.org/api/modules.html#modules_caching)ので大きなパフォーマンスの低下はないはずです。

[実際のソースコード](https://github.com/joyent/node/blob/master/lib/module.js#L280)

### 方法3：dependency injection

[dependency injection(DI; 依存性の注入)](http://ja.wikipedia.org/wiki/%E4%BE%9D%E5%AD%98%E6%80%A7%E3%81%AE%E6%B3%A8%E5%85%A5)は、モジュール間の結合度を下げるためのデザインパターンの一種です。

「モジュールBがモジュールAを利用する」という依存関係をソースコードにハードコードするのではなく、外部からモジュールBの引数に注入しています。こうすることで、b.jsはa.jsをrequireする必要がなくなるということです。

上の例だとモジュールのI/Fに若干の変更は入りますが、DIのテクニックを活用することで、モジュール間の結合度が下がり、モジュールのテストが書きやすくなるので、こちらもいい方法なのかなと思います。

### まとめ

node.js における circular dependency という問題とその対処法について紹介しました。一度この問題にハマって解決方法を知るとそれ以降は用心深くなれるのですが、知らないとかなり苦労します。まだこの問題にハマっていない方も是非知っておいて損はないと思います！

### Reference

  * [Circular dependency &#8211; Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Circular_dependency)
  * [node.js and circular dependencies](http://selfcontained.us/2012/05/08/node-js-circular-dependencies/)
  * [module &#8211; How to deal with cyclic dependencies in Node.js &#8211; Stack Overflow](http://stackoverflow.com/questions/10869276/how-to-deal-with-cyclic-dependencies-in-node-js)