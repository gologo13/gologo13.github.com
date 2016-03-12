---
id: 838
title: '東京Node学園祭2014 #nodefest'
date: 2014-11-19T08:25:38+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=838
permalink: /2014/11/19/tokyo-nodefest-2014/
s4_url2s:
  - 
s4_image2s:
  - 
s4_ctitle:
  - 
s4_cdes:
  - 
categories:
  - node.js
---
[<img src="http://www.gologo13.com/wp-content/uploads/2014/11/nodeconf-300x245.jpg" alt="" width="300" height="245" class="aligncenter size-medium wp-image-855" />](http://www.gologo13.com/wp-content/uploads/2014/11/nodeconf.jpg)

[東京Node学園祭2014](http://nodefest.jp/2014/)に参加してきました。

感想ですが、Node学園祭には初参加でしたが、色んな発表を見れたので勉強になりました。海外スピーカーの発表を中心に聞いていました。そこまで聞き取れたわけではないので、リスニングの勉強の必要性を痛感しました。。 次は何らかの形で発表できたらなと思います。

Node.jsコミッターを多く抱えている[Strongloop](strongloop.com) CEOの[Issac Roth(@ijroth)さん](https://twitter.com/ijroth)に英語で話して、グッズをもらえたのはいい思い出です。

以下は各発表の感想と資料をリンクしています。

<!--more-->

## nodeschool in Japan @maxogden

[NodeSchool Tokyo](http://nodeschool.io/tokyo/) で公開されているチュートリアルを解いていくワークショップでした。

<pre># node.jsの基本的なチュートリアル
$ npm install -g learnyounode-jp
$ learnyounode

# browserifyのチュートリアル
$ npm install -g browserify-adventure-jp
$ browserify-adventure

# LevelDBのチュートリアル
$ npm install -g levelmeup-jp
$ levelmeup
</pre>

ちなみに、これらのツールは[workshopper](https://github.com/rvagg/workshopper)というツールで作られています。これらのチュートリアルはもともと英語で作成されているので、日本語に翻訳してくれる人を絶賛募集中みたいです。

## workshop &#8211; socket.io v1.0 @TonyKovanen

[socket.io-workshop-full](https://github.com/rase-/socket.io-workshop-full)

socket.ioを使った3Dゲームをライブコーディングで作るというワークショップでした。Twitter上の盛り上がりもすごかったです。私は参加できませんでしたが、ソースコードが勉強になるようなのであとで眺めてみたいと思います。

## What’s coming in Node, Express & LoopBack @ijroth

StrongLoop CEO の発表でした。Node 0.12で導入される新機能の紹介が主で、StrongLoopで開発している[loopback](http://loopback.io/)というフレームワークの紹介もありました。

Nodeの並列モデルがv0.12からは **dispatcher model**, 将来には **single process model** になるみたいです（[これ](http://strongloop.com/strongblog/whats-new-node-js-v0-12-multiple-context-execution/)のことかな）。 また、v0.12からは generator がデフォルトで使えるようになって、コールバック地獄にならない書き方ができようになります。 あとは、[Zone](https://github.com/strongloop/zone)という機能が使えるようになれば、エラー発生時に詳細なスタックトレースが出力でき、デバッグが用意になりそうです。

LoopbackはIsomorphicなフレームワークの１つなのですが、個人的に少し使っていて

<pre>$ slc loopback:model User
</pre>

のようにモデルを作成するだけで、Rest APIが自動生成されるのには驚きました。explorerという機能があるのですが、これを使えば自動生成されたAPIの動作確認が簡単にできます。

最初の学習コストは少し高いかもしれませんが、[ドキュメント](http://docs.strongloop.com/display/public/LB/LoopBack)が充実しているので、使いこなせれば効率的な開発ができそうです。Loopbackについて勉強するには、こちらの[チュートリアル](https://gist.github.com/bajtos/7aaf713305060a7ee895)がオススメです。

Loopbackについては今絶賛勉強中なので、いずれ使い方についてブログでまとめたいと思います。

## node.js for beginners, grunt gulp browserify webpack bower @ahomu

発表者の[ブログ](http://havelog.ayumusato.com/misc/e633-nodefest_2014.html) にもありますが、パッケージ管理ツールである`npm`や`browerify`、タスク実行ツールである`grunt`や`gulp`、そしてモジュール管理ツールである`browserify`, `webpack`, `duo` といったツールの紹介が主な内容でした。

## Node-v0.12のTLSを256倍使いこなす方法 @jovi0608

<div style="margin-bottom:5px">
  <strong> <a href="//www.slideshare.net/shigeki_ohtsu/node-fest2014-ohtsu" title="Node-v0.12のTLSを256倍使いこなす方法" target="_blank">Node-v0.12のTLSを256倍使いこなす方法</a> </strong> from <strong><a href="//www.slideshare.net/shigeki_ohtsu" target="_blank">shigeki_ohtsu</a></strong>
</div>

Node.js v0.12ではTLSの処理が大きく改善されたという話。今年は[HeartBleed](http://heartbleed.com/)や[Poodle](http://en.wikipedia.org/wiki/POODLE) といったSSL/TLSに関連した脆弱性が多く見つかる当たり年であり、SPDYベースのHTTP/2がTLSを必須にしているということもあって、ますますTLSの重要性が増してきています。

この発表ではSSL False Start, OCSP Stapling, TLS Ticket といったTLS関連の技術について知ることができたので、すごく勉強になりました。SSL False Start, OCSP Staplingについては[ここ](http://d.hatena.ne.jp/tkng/20130108/1357610340)を合わせて読むと理解が深まりました。

## すべてのノードトランスパイラーがひどい！ならば、ノードトランスパイラーをいかに改善できるか。 @leichtgewicht

<div style="margin-bottom:5px">
  <strong> <a href="//www.slideshare.net/leichtgewicht/nodefest2014-transpiler" title="NodeFest2014 - Transpiler" target="_blank">NodeFest2014 &#8211; Transpiler</a> </strong> from <strong><a href="//www.slideshare.net/leichtgewicht" target="_blank">Martin Heidegger</a></strong>
</div>

この発表は聞けませんでしたが、JavaScript界隈で使われている Transpiler というソースコードからソースコードへの変換器についての話のようです。

## Node Past, Present, Future @mikeal

資料見つからず。[request/request](https://github.com/request/request)の作者の発表です。

あまり英語が聞き取れませんでしたが、書いているProxyサーバのソースコードの行数が時代とともに短くなっていった話。 Past, Present, Future はそれぞれ以下の対応なのかなと。

  * Past が callback
  * Present が[stream](http://nodejs.org/api/stream.html)
  * Future が [generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*) 
      * [co](https://github.com/tj/co)を使えばより簡単にgeneratorを扱える

## テスト用ライブラリ power-assert, その開発で学んだ npm モジュール設計の勘所 @t_wada

<div style="margin-bottom:5px">
  <strong> <a href="//www.slideshare.net/t_wada/power-assert-nodefest-2014" title="power-assert, mechanism and philosophy" target="_blank">power-assert, mechanism and philosophy</a> </strong> from <strong><a href="//www.slideshare.net/t_wada" target="_blank">Takuto Wada</a></strong>
</div>

この発表は聞けませんでしたが、資料が公開されていたのでリンクだけ。

## ギャルでもゎかる node-webkit @upgrade_ayp

資料見つからず。すごく個性的な発表であまり頭に入りませんでした 笑。

## Node.jsで操るKurentoメディアサーバー @massie_g

<div style="margin-bottom:5px">
  <strong> <a href="//www.slideshare.net/mganeko/nodekurento" title="Nodeで操るKurentoメディアサーバー ( Kurento + WebRTC + Node.js )" target="_blank">Nodeで操るKurentoメディアサーバー ( Kurento + WebRTC + Node.js )</a> </strong> from <strong><a href="//www.slideshare.net/mganeko" target="_blank">mganeko</a></strong>
</div>

この発表も聞けませんでしたが、[WebRTC](http://ja.wikipedia.org/wiki/WebRTC)についての発表みたいです。 Node.jsが関係あるとすれば、WebRTCにおけるシグナリングという処理をWebSocketのプロトコル上で行うが、ここにsocket.ioが使えるよというところでしょうか。あとでじっくり読みたい。

## 参考

  * [Togetterまとめ](http://togetter.com/li/745684)