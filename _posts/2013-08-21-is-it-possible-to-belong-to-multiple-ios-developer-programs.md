---
id: 640
title: iOS Developer Progamで複数チームに所属することは可能か？
date: 2013-08-21T00:39:48+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=640
permalink: /2013/08/21/is-it-possible-to-belong-to-multiple-ios-developer-programs/
categories:
  - ios
  - mac
  - tips
---
[<img src="http://www.gologo13.com/wp-content/uploads/2013/08/multiple-developer-programs.png" alt="" width="1294" height="365" class="aligncenter size-full wp-image-641" />](http://www.gologo13.com/wp-content/uploads/2013/08/multiple-developer-programs.png)

iOS Developer Progamで複数チームに所属することは可能か？

結論としては、可能です。

添付したスクリーンショットのように、iOS dev center にログインするたびに、どのチームで操作を行うかを選択することができる。

すでにあるチームの Developer Program に所属している状態で、新規で Developer Program に参加しようとした時、

  * 古いチームの情報が上書きされてしまい、無効になる
  * 既にチームに参加しているから、新規で参加できない

と、懸念があったが、全くそんなことはなかった。

個人的に安心できたので、シェアします。

* * *

以下、実機インストールまでの簡単な導入手順

  1. Safari で iOS Dev Center を開く（Chrome だとうまく行かないことがあった）
  2. デバイス登録：実機インストールするデバイス名, UDID(Xcode Identifier で調べられる）を登録
  3. AppID 登録：アプリのユニークなIDの作成
  4. 証明書登録：KeyChain Access で作成できる
  5. プロビジョニングプロファイル作成：実機インストールするための準備ファイル

詳しくは、[ここ](http://www.matchyo.net/mblog/?p=8026) が参考になりそう。