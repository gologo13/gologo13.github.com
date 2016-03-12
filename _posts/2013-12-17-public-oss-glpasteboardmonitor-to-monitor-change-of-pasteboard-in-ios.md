---
id: 679
title: iosのクリップボードの変化を検知するOSS「GLPasteboardMonitor」を公開しました
date: 2013-12-17T01:10:27+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=679
permalink: /2013/12/17/public-oss-glpasteboardmonitor-to-monitor-change-of-pasteboard-in-ios/
categories:
  - ios
  - objective-c
  - OSS
---
 https://github.com/gologo13/GLPasteboardMonitor 

iOS のクリップボード(UIPasteboard の generalPasteboard)の変化を検知し、通知が受け取れるようにするOSS「GLPasteboardMonitor」を公開しました。

使い方は github に書いてあるので、よかったら使ってみてください。 あまり大したことはしていないのですが、ポイントを上げるとすると、

  1. バックグラウンドでも変化を検知できるように、 _Task Competion_ を使っている点
  2. 画像データの比較で、単純なバイト列の比較ではなく、ハッシュ値を元に比較し、比較を高速にしている点

です。

サンプルのプロジェクトでは、クリップボードの変化を検知すると、Local Notification を飛ばすようになってます。