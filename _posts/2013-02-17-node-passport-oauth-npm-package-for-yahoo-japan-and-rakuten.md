---
id: 453
title: Open Hack Day でnode.jsのPassportを使ってYahoo!JAPANと楽天のOAuth認証モジュールを作った
date: 2013-02-17T00:13:50+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=453
permalink: /2013/02/17/node-passport-oauth-npm-package-for-yahoo-japan-and-rakuten/
categories:
  - node.js
  - oauth
  - Uncategorized
---
[<img src="http://www.gologo13.com/wp-content/uploads/2013/02/summary-logo.png" alt="" title="summary-logo" width="187" height="154" class="aligncenter size-full wp-image-458" />](http://www.gologo13.com/wp-content/uploads/2013/02/summary-logo.png)

## 概要

今週の土日に開催された [Open Hack Day Japan](http://yhacks.jp/hackday/) という Hackathon イベントに参加して来ました。主催は Yahoo! JAPAN です。会社の同期と二人で参加しました。

## 紹介(Passport)

[<img src="http://www.gologo13.com/wp-content/uploads/2013/02/スクリーンショット-2013-02-18-0.58.011.png" alt="" title="スクリーンショット 2013-02-18 0.58.01" width="417" height="129" class="aligncenter size-full wp-image-457" />](http://www.gologo13.com/wp-content/uploads/2013/02/スクリーンショット-2013-02-18-0.58.011.png)

私たちがつくったものは node.js で OAuth 認証を超簡単に実装できるモジュールです。このモジュールは [Passport](http://passportjs.org/) という OAuth 認証モジュールのラッパーのような形で提供しています。

現在、Facebook, Twitter 等の数多くのウェブサービスのラッパーが提供されており、今回新たに Yahoo!JAPAN と楽天のラッパーを作成したという位置付けです。

## 成果物

  * GitHub 
      * [Yahoo! JAPAN 用 OAuth 認証モジュール(passport-yj)](https://github.com/Lewuathe/passport-yj)
      * [楽天用 OAuth 認証モジュール(passport-rakuten)](https://github.com/gologo13/passport-rakuten)
  * npm 
      * [passport-yj](https://npmjs.org/package/passport-yj)
      * [passport-rakuten](https://npmjs.org/package/passport-rakuten)

## 使い方

yconnect を例に使い方を説明したいと思います。 リポジトリの examples/login/app.js で簡単に試せます。

  * [Lewuathe/passport-yj · GitHub](https://github.com/Lewuathe/passport-yj)

### 1.アプリケーション登録

[Yahoo!デベロッパーネットワーク](http://developer.yahoo.co.jp/) からアプリケーション登録します。

  * アプリケーションID
  * シークレット

を取得します。ちゃんとコールバックURIも登録します。

### 2. インストール

リポジトリを git clone して、config.js というファイルを編集します。 先ほど取得したアプリケーションID、シークレット、コールバックURIを書いてください。 そして、npm install で依存モジュールをインストールします。

<pre class="brush: shell">$ cd ~
    $ git clone git clone git@github.com:Lewuathe/passport-yj  
    $ vim ~/passport-yj/config.js
    module.exports = {
        client_id: "あなたのアプリケーションID",
        client_secret: "あなたのシークレット",
        redirect_uri: "あなたのコールバックURI"
    }
    $ cd ~/passport-yj/examples/login
    $ npm install
</pre>

### 3. 起動

あとは express を起動するだけです。

<pre class="brush: shell">$ node app
</pre>

これで http://localhost:3000 にアクセスすれば試すことができます。

## 今後

ただひとつ問題があります。yconnect でアクセストークンを取得するときに、client ID と client secret を Authorization ヘッダに付与して Basic 認証を行なうという仕様になっています。しかしながら、この認証方法は他の OAuth2.0 の実装と比較して特殊で、node の oauth モジュールがこの認証方式に対応していません。

そのため、passport-yj では npm の postinstall の時に oauth モジュールの oauth2.js にパッチを当てるという処置を暫定的に行なっています。

もちろん、このような処置はあまりイケていないので、oauth モジュールの作者に Pull Request を送って、エレガントにこの問題を解決したいと思います（続く&#8230;かも）。


<ins datetime="2013-02-20T16:11:00+00:00"> 2013/02/21 1:17<br /> Pull Request 送りました！<br /> <a href="https://github.com/ciaranj/node-oauth/pull/126">Client Authentication via Basic Authorization, not body by gologo13 · Pull Request #126 · ciaranj/node-oauth</a> </ins> 

  


## まとめ

  * Yahoo!JAPANと楽天向けの Passport を使った OAuth 認証モジュールの開発
  * GitHub で OSS として公開！
  * npm モジュールとして公開！