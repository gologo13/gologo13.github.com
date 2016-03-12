---
id: 591
title: shellで新しくコマンドをインストールしたときにCommand not foundとなる問題を解決する方法
date: 2013-05-17T01:53:59+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=591
permalink: /2013/05/17/solution-to-resolve-command-not-found-in-shell/
categories:
  - cui
  - shell
tags:
  - bash
  - cui
  - shell
---
例えば、hoge という実行プログラムを PATH が通っている /usr/local/bin/ に新しくインストールしたとします。

<pre class="lang:sh decode:true " >$ hoge</pre>

と実行すると Command not found: hoge と言われる。

こういう経験よくありませんか？

そんな致命的な問題ではないのですが、この問題に割りとよく悩まされていて、私はよく新しく端末を立ち上げるか、exec zsh とかしてました。 でも、

<pre class="lang:sh decode:true " >$ hash -r
</pre>

と実行することで解決出来ます。 shell の内部にあるコマンドのハッシューテーブルを再構築するコマンドのようです。 すっきり。