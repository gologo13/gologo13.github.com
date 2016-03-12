---
id: 746
title: NSSetの内部実装
date: 2014-03-07T00:07:41+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=746
permalink: /2014/03/07/implementation-of-nsset/
categories:
  - algorithm-and-data-structure
  - ios
  - objective-c
  - Uncategorized
---
NSSet の内部実装

ふと気になったので調べてみたところ、以下のリンクを見つけた。

  * [objective c &#8211; NSSet implementation &#8211; Stack Overflow](http://stackoverflow.com/questions/5863510/nsset-implementation)

どうやら実装としてはハッシュテーブルらしい。だから、要素の挿入、削除、検索が一定時間でできる。

なんでそんなことがわかるかというと、NSSet のC言語実装である CFSet が CFHashTable というハッシュテーブルを使って書かれているから。

実は CoreFoundation のソースコードは公開されていて、その一部である CFSet のソースコードも見ることができる。

  * [CoreFoundation](http://opensource.apple.com/source/CF/CF-550.42/)
  * [CFSet.h](http://opensource.apple.com/source/CF/CF-550.42/CFSet.h)
  * [CFSet.c](http://opensource.apple.com/source/CF/CF-550.42/CFSet.c)

CFSet のメソッドを見ていると、NSSet のどのメソッドと対応しているか、それとなくわかる。気になる実装を軽く眺めてみるだけでも楽しいかも。もしかしたら、CoreFoundation のクラスの内部でクラッシュした時に、参考になるかも（笑）