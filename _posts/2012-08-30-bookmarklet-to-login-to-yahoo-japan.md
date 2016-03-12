---
id: 81
title: ワンクリックで Yahoo! に簡単にログインするブックマークレット
date: 2012-08-30T19:48:53+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=81
permalink: /2012/08/30/bookmarklet-to-login-to-yahoo-japan/
categories:
  - javascript
---
もし、あなたが複数の Yahoo! JAPAN アカウントを持っている場合、別のアカウントに切り替えるのに、いちいちIDとパスワードを打つのが面倒だと感じたことはありませんか？
  
そんな課題を解決してくれるブックマークレットを紹介します。

例えば、あなたの ID とパスワードが

  * ID: test
  * パスワード: password

であるとすると、次のようなブックマークレットを登録すればいいだけです。
  
赤字の部分をあなたの ID とパスワードに置き換えてください。

<p style="border-style: dotted;">
  javascript:var%20u=&#8217;<span style="color: #ff0000;">test</span>&#8216;;var%20p=&#8217;<span style="color: #ff0000;">password</span>&#8216;;document.getElementById(&#8216;username&#8217;).value=u;document.getElementById(&#8216;passwd&#8217;).value=p;document.getElementsByName(&#8216;login_form&#8217;)[0].submit();void(0);
</p>

この方法だと、余計なアドオンやソフトウェアをインストールする必要はありません。

## ブックマークレットの登録方法

登録方法は適当なページをお気に入りに追加して、その URL を上の JavaScript に書き換えるだけです。
  
詳しくは、 [ここ](http://www.hatena.ne.jp/tool/bookmarklet)へ。

## ブックマークレットの使い方

下の画像のような、ヤフーのログイン画面をブラウザで開いているときに、登録したブックマークレットをクリックすると、簡単にログインできます！たったのワンクリックです！

例えば、test1 と test2 という複数のアカウントを使い分けるときには、下の画像のようにブックマークレットに登録しておくと便利です！

[<img src="http://www.gologo13.com/wp-content/uploads/2012/08/yahoo2.png" alt="" title="yahoo2" width="415" height="91" class="aligncenter size-full wp-image-307" />](http://www.gologo13.com/wp-content/uploads/2012/08/yahoo2.png)

念の為、述べておきますが、このブックマークレットのURLを見れば、パスワードがわかってしまうので、共用の PC のブラウザにこのブックマークレットを登録することはおすすめしません。

ちなみ、ブックマークレットに favicon を表示させるには [「Bookmark Favicon Changer」](http://mozilla-remix.seesaa.net/article/230823667.html "「Bookmark Favicon Changer」") というアドオンを使用しました。