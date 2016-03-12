---
id: 668
title: dispatch_create_queueを使うときの勘違い
date: 2013-12-15T13:48:30+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=668
permalink: /2013/12/15/misunderstanding-about-dispatch-create-queue-in-gcd/
categories:
  - gcd
  - ios
  - objective-c
---
久々エントリ。

queue を作るとき、dispatch\_create\_queue の第１引数に名前を指定する。 ところが、**すでに同じ名前の queue があるからといって、その queue が再利用されるわけではない**。

例えば、以下のコードは**queueの生成コストがすごく無駄**。

<pre class="lang:default decode:true " >for (NSInteger i = 0 ; i &lt; 100; ++i) {
    dispatch_queue_t queue = dispatch_queue_create(“com.gologo13.gcd”, DISPATCH_QUEUE_SERIAL);
    dispatch_async(queue, ^{
        NSLog(@"%d", i);
    });
}</pre>

ドキュメントに書いてあるけど、このラベルは本質的に意味はなくて、デバッグ時の queue の識別子として使われるだけであった。

label

A string label to attach to the queue to uniquely identify it in debugging tools such as Instruments, sample, stackshots, and crash reports. Because applications, libraries, and frameworks can all create their own dispatch queues, a reverse-DNS naming style (com.example.myqueue) is recommended. This parameter is optional and can be NULL.

だから、上のソースコードは「１個のキューに対して、１００個のタスクが直列に実行」されるわけではなく、「１００個のキューに対して、１個のタスクが直列に実行」される。よって実質的には並列キューみたいにタスクが実行される。

### 参考

  * [Concurrency Programming Guide: Dispatch Queues](https://developer.apple.com/library/ios/documentation/General/Conceptual/ConcurrencyProgrammingGuide/OperationQueues/OperationQueues.html)
  * [ConcurrencyProgrammingGuide.pdf](https://developer.apple.com/jp/devcenter/ios/library/documentation/ConcurrencyProgrammingGuide.pdf)
  * [8.2 Grand Central Dispatch · mixi-inc/iOSTraining Wiki](https://github.com/mixi-inc/iOSTraining/wiki/8.2-Grand-Central-Dispatch)
  * [UITableViewCellの再利用と非同期処理の話。 &#8211; Togetterまとめ](http://togetter.com/li/601490) ←合わせて読みたい