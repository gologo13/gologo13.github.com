---
id: 563
title: ワンクリックで楽天に簡単にログインするブックマークレット
date: 2013-04-14T12:15:48+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=563
permalink: /2013/04/14/bookmarklet-to-login-to-rakuten/
categories:
  - lifehack
tags:
  - bookmarklet
  - JavaScript
---
## 概要

以前、Yahoo!JAPANにワンクリックでログインする方法を紹介しました。

  * [ワンクリックで Yahoo! に簡単にログインするブックマークレット | Now or Never](http://www.gologo13.com/2012/08/30/bookmarklet-to-login-to-yahoo-japan/)

今回はその**楽天**版について紹介します。 このライフハックにより、楽天にログインするための**面倒なID入力、パスワード入力が不要**になります。

## 登録方法

もしあなたの楽天IDとパスワードがそれぞれ

  * ID: hoge@yahoo.co.jp
  * Password: mypassword

の場合、以下のような**ブックマークレット**を作成すればOK。ブックマークに登録するとき、ID とパスワードの部分はあなたのものに書き換えて、登録してください。

<pre class="lang:js decode:true " title="bookmarklet" >javascript:document.getElementById('userid').value='hoge@yahoo.co.jp';document.getElementById('passwd').value='mypassword';document.getElementsByName('login')[0].submit();void(0);</pre>

ブックマークは本来「http://&#8230;」から始まる URL を登録しますが、「javascript:&#8230;」から始めることで JavaScript として実行されます。これを**ブックマークレット**と呼びます。

補足： 使用しているプラグインが改行を自動挿入してくれません。 ブックマークレットを全選択したい場合は、お手数をお掛けしますが、 ブックマークレットの部分をマウスオーバーして、出現する一番右のボタンをクリックしてください。 クリックすると、別タブでブックマークレット全体を表示してくれて、全選択しやすいと思います。

## 使用方法

[<img src="http://www.gologo13.com/wp-content/uploads/2013/04/Screen-Shot-2013-04-14-at-12.03.16-300x229.png" alt="Screen Shot 2013-04-14 at 12.03.16" width="300" height="229" class="aligncenter size-medium wp-image-567" />](https://www.rakuten.co.jp/myrakuten/login.html)

あとはこの画面にいって、登録したブックマークをクリックするだけでOKです。

もちろんこのブックマークレットはPCのブラウザだけでなく、スマホのブラウザでも動作します！ ログインのめんどくささにお困りの方はぜひお試しください。

念の為、述べておきますが、このブックマークレットのURLを見れば、パスワードがわかってしまうので、共用の PC のブラウザにこのブックマークレットを登録することはおすすめしません。

## 要望募集

他にも「このサイトにワンクリックでログインしたい！」という要望があればぜひコメントください！