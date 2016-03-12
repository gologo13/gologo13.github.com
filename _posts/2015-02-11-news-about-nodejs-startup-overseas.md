---
id: 962
title: 海外のNode.js系スタートアップのニュースを紹介
date: 2015-02-11T22:47:04+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=962
permalink: /2015/02/11/news-about-nodejs-startup-overseas/
s4_url2s:
  - 
s4_image2s:
  - 
s4_ctitle:
  - 
s4_cdes:
  - 
categories:
  - Uncategorized
---
今日は今までと雰囲気を変えて、Node.js 系スタートアップに関するニュースを紹介します。

## Nodejitsu が GoDaddy にジョイン

[<img src="http://www.gologo13.com/wp-content/uploads/2015/02/godaddy.png" alt="" width="537" height="180" class="aligncenter size-full wp-image-963" />](http://www.gologo13.com/wp-content/uploads/2015/02/godaddy.png)

  * [Nodejitsu joins GoDaddy | Nodejitsu Inc.](http://blog.nodejitsu.com/nodejitsu-joins-godaddy/)
  * [Nodejitsu to join the GoDaddy team](https://garage.godaddy.com/godaddy/nodejitsu-join-godaddy-team/?linkId=12275397)
  * [Why GoDaddy&#8217;s Nodejitsu deal is great for Node.js | VentureBeat | Dev | by Jordan Novet](http://venturebeat.com/2015/02/10/why-godaddys-nodejitsu-deal-is-great-for-node-js/)

これは昨日発表されたニュースです。 [Nodejitsu](https://www.nodejitsu.com/)はHerokuのようなPaaSを提供しているスタートアップです。 Nodejitsuが公開している有名なnpmパッケージとしては [forever](https://github.com/foreverjs/forever), [node-http-proxy](https://github.com/nodejitsu/node-http-proxy), [winston](https://github.com/winstonjs/winston), [flatiron.js](http://flatironjs.org/) がありますね。forever は node.js をデーモン化するために使ってる人も多いのではないでしょうか。node-http-proxy はプロキシとして定番ですね。 Nodejitsuが元々やっていたサービスは提供をやめるそうですが、Node.jsコミュニティへの貢献は引き続き行うと表明しています。

一方で、[GoDaddy](https://www.godaddy.com/)はドメイン登録、VPS、サーバホスティング、SSL証明書の発行といった、日本で言うお名前ドットコム的な存在ですね。GoDaddyは元々インフラを.Netで開発していて、インフラのサーバ台数を削減させるためにNode.jsに切り替えているんだそうです。このタイミングで、Node.jsのプロフェッショナルを多く抱えているNodejitsuを買収することで、Node.jsの開発力を高める狙いが合ったと見られます。また、GoDaddyは[StrongLoop](http://strongloop.com/)というNode.jsによるmBaaSを提供しているスタートアップを自社のAPI基盤として採用したことも[昨日ニュースになりました](http://strongloop.com/strongblog/godaddy-api-platform/)。

## Joyent が Node.js Foundation を設立

[<img src="http://www.gologo13.com/wp-content/uploads/2015/02/Joyent-logo-1024x278.png" alt="" width="640" height="174" class="aligncenter size-large wp-image-965" />](http://www.gologo13.com/wp-content/uploads/2015/02/Joyent-logo.png)

こちらも昨日発表されたニュースです。 Node.jsを管理していて、Node.jsによるクラウドサービスを提供している[Joyent](https://www.joyent.com)がIBM, Microsoft, PayPal, SAP, Linux Foundationなどと協力してNode.jsコミュニティでopen governance modelを進めるための組織の設立を[発表しました](https://www.joyent.com/about/press/joyent-moves-to-establish-nodejs-foundation)。

Joyentは[io.js](https://iojs.org/en/index.html)というNode.jsのforkが出たこともあり、コミュニティからの求心力が下がっていました。 今回の発表で open governance model つまり議論をオープンにし、コミュニティの意見を尊重しますよという姿勢を見せることで、改めて求心力を取り戻そうという狙いが見えます。 ちなみに、io.js も同様に open governance model を採用しています。 今後 Joyent 側がどういう動きを取るか注目です。

## NodeSourceの資金調達

[<img src="http://www.gologo13.com/wp-content/uploads/2015/02/nodesource_identityRGB_vertical.png" alt="" width="268" height="155" class="aligncenter size-full wp-image-967" />](http://www.gologo13.com/wp-content/uploads/2015/02/nodesource_identityRGB_vertical.png)

Node.jsの開発ツールやトレーニング、コンサルサービスを提供するスタートアップである[NodeSource](https://nodesource.com/)が[VCから3百万ドルの資金調達](http://techcrunch.com/2015/02/09/nodesource-raises-3-million-to-build-new-programming-tools/)を実現させました。 低コストでハイパフォーマンスなWebサーバであるNode.jsを導入してみたいという企業は多そうなので、今後もこういったサービスの需要は増えそうですね。

## まとめ

Node.jsは今後も熱い！