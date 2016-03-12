---
id: 870
title: Loopbackフレームワーク入門
date: 2014-12-09T23:53:58+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=870
permalink: /2014/12/09/nodejs-loopback/
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
[<img src="http://www.gologo13.com/wp-content/uploads/2014/12/loopback.jpg" alt="" width="300" height="300" class="aligncenter size-full wp-image-879" />](http://www.gologo13.com/wp-content/uploads/2014/12/loopback.jpg)

[Node.js Advent Calendar 2014](http://qiita.com/advent-calendar/2014/nodejs)の9日目の記事です。 ブログ記事を上げるのが遅くなってすみません。

今回は、Node.jsのWAFである[LoopBack](http://loopback.io/)の使い方について簡単に紹介しようと思います。使ってみた感触としては、ORMがすごく優秀で、RestAPIを自動で生成してくれたりと非常に強力なフレームワークだと感じました！では紹介していきます。

<!--more-->

## loopback とは

loopback とは [StrongLoop](strongloop.com) という mBaaS (Mobile Backend as a Service) を事業としている会社がOSSとして公開しているNode.js の isomorphic な Webフレームワークのことです。

[公式ページ](http://loopback.io/)に書かれている特徴は以下のとおりです。

<pre>LoopBackは高い拡張性があるNode.jsのフレームワークである

- 動的なRestAPIを生成するためにコマンドラインが利用できるよ
- デバイスとブラウザをデータとサービスに接続できる ※iPhone SDK, Android SDKがあるのでアプリ開発にも使えます
- プッシュ通知、ファイル管理、サードパーティログイン、位置情報と連携できる
- オンプレミス（自社サーバ）でもクラウドでも使えます
- StrongLoop Studio API Composer を使えば、LoopBackアプリを見た目で操作できるよ
- APIをセキュアに管理するために、Loopback API gateway をAPIクライアントとPIサーバの中継サーバとして使えます
</pre>

## インストール

まずは generator-loopback をインストールします。 プロジェクトのディレクトリを作成後に、yo で loopback の雛形を生成します。

<pre>$ npm i -g generator-loopback
$ mkdir sample &#038;&#038; cd sample
$ yo loopback
</pre>

## loopback のディレクトリ構成、ファイル説明

yo で雛形を生成すると、以下のようなディレクトリ構成になっています。

<pre>.
├── client
│   └── README.md
├── package.json
└── server
  ├── boot
  │   ├── authentication.js
  │   ├── explorer.js
  │   ├── rest-api.js
  │   └── root.js
  ├── config.json        ... RestAPIに関する設定（ホスト名、ポート番号を記述）
  ├── datasources.json   ... データベースに関する設定（DB名、ホスト名などを記述）
  ├── model-config.json  ... モデル管理設定
  └── server.js          ... loopbackの本体ファイル
</pre>

server/server.js の中身を見てみれば、`app.use(loopback.favicon());`といったコードがあります。[express](http://expressjs.com/)と似てますが、実はloopbackはexpressを内部で利用しているフレームワークなのです。

## モデル

loopbackにおいてモデルは非常に重要で、モデルはデータベースに対するORMです。loopbackのモデルは、MongoBD, MySQL, Oracleといったデータベース製品を抽象化できます（後述）。

loopbackのすごい点は、**モデルを作るだけでRest APIも生成される**という点です。経験的にWebAPIの開発において、DBモデルを作ったあとはそれを操作するためのAPI(GET, POST, PUT, DELETE)などを作成しますよね。こういったルーチンワークが自動化されるというのは本当に素晴らしいことだと思います。

では、以下では実際にモデルを作ってみます。ちなみに、[Users](http://docs.strongloop.com/display/public/LB/Using+built-in+models)というモデルは事前に定義されています。

まず、Bookmark という名前のモデルを作成します。 `yo loopback:model` を実行するとインタラクティブなシェル上が立ち上がり、モデルの情報の入力が促されます。 以下の例では、`title`プロパティと`url`プロパティを追加しています。

<pre>$ yo loopback:model Bookmark
? Enter the model name: Bookmark （&lt;-モデル名）
? Select the data-source to attach Bookmark to: db (memory)　（&lt;-データの保存場所）
? Select model's base class: PersistedModel　（&lt;-モデルの継承クラス）
? Expose Bookmark via the REST API? Yes　（&lt;-モデルをRestAPIとして公開するか？）
? Custom plural form (used to build REST URL):
Let's add some Bookmark properties now.

Enter an empty property name when done.
? Property name: title
invoke   loopback:property
? Property type: string
? Required? Yes

Let's add another Bookmark property.
Enter an empty property name when done.
? Property name: url
invoke   loopback:property
? Property type: string
? Required? Yes

Let's add another Bookmark property.
Enter an empty property name when done.
? Property name:
</pre>

１つ選択に迷うポイントとしては、`Select model's base class:` のところで [Model](http://docs.strongloop.com/display/public/LB/Basic+model+object)か[PersistedModel](http://docs.strongloop.com/display/public/LB/PersistedModel+class) のどちらを選ぶべきかというところです。

違いとしては、Modelは[モデルデータの変更や削除があった場合にコールバックを実行する](http://docs.strongloop.com/display/public/LB/Model+hooks)ことができたり、[モデルデータにスキーマ定義に反するデータ型を代入しようとした時に、エラーを発生してくれるvalidation機能](http://docs.strongloop.com/display/public/LB/Validating+model+data)であったりを提供しています。 一方で、PersistedModel は Model を継承したモデルクラスで、Modelで定義されたメソッドに加えて、データベース操作のためのCRUD機能をサポートします。どういったメソッドがあるかは[ここ](http://docs.strongloop.com/display/public/LB/PersistedModel+class)で確認できます。 なので、モデルをデータベースと対応させるなら、**PersistedModel** を選択すればOK。

モデルの説明は以上にして、モデルを生成すると、トップディレクトリに `common` というディレクトリが作成されて、ここにモデルの定義ファイルが２つ配置されます。loopback は isomorphic なフレームワークであるので、LoopbackとAngular.jsと組み合わせ使うときはこのモデルファイルはブラウザJSとサーバサイドJS(node.js)とで共有されます。

<pre>.
├── client
├── package.json
├── server
└── common/
  └── models
    ├── bookmark.js　（&lt;-NEW!)
    └── bookmark.json　（&lt;-NEW!)
</pre>

新しく生成されたファイルの中身を見てみましょう。 bookmark.json はモデルのスキーマ定義です。入力したカラムの情報が定義されてますね。

<pre>$ cat common/models/bookmark.json
{
  "name": "Bookmark",
  "base": "PersistedModel",
  "idInjection": true,
  "properties": {
    "title": {
      "type": "string",
      "required": true
    },
    "url": {
      "type": "string",
      "required": true
    }
  },
  "validations": [],
  "relations": {},
  "acls": [],
  "methods": []
}
</pre>

次に、bookmark.js はモデルの実装ファイルです。この時点では実装がないように見えますが、先ほど紹介したModelであったり、PersistedModelのメソッドを呼び出すことができます。もちろんここに独自のロジックメソッドを追加することも可能です [参考](http://docs.strongloop.com/display/public/LB/Remote+methods)。

<pre>$ cat common/models/bookmark.js
module.exports = function(Bookmark) {

};
</pre>

## Relation

モデルの [Relation](http://docs.strongloop.com/display/public/LB/Creating+model+relations) も yo コマンドで生成することができます。 1対1、1対多、多対多の関係を作ることができます。

先ほど作った Bookmark モデルに加えて、Page モデルがあるとします。 Page は複数の Bookmark を持つことができるとします。 すると、Relation は以下のように作れます。

<pre>$ yo loopback:relation
? Select the model to create the relationship from: Page
? Relation type: has many （&lt;-関係）
? Choose a model to create a relationship with: Bookmark
? Enter the property name for the relation: bookmarks
? Optionally enter a custom foreign key:
? Require a through model? No　（&lt;-交差テーブルを持つかどうか）
</pre>

relationを作ると、PageモデルのJSONスキーマにその関係が追記されます。 また、relationを作ると、`GET /Pages/{id}/bookmarks`といった具合にモデルに紐づくリレーションも考慮して、RestAPIを生成してくれます。すごく気が利いてますね。

<pre>$ cat common/models/page.json
less page.json
{
  "name": "Page",
  "base": "PersistedModel",
  ...(略)...
  "relations": {
    "bookmarks": {
      "type": "hasMany",
      "model": "Bookmark",
      "foreignKey": ""
  }
}
</pre>

## Explorer

[[<img src="http://www.gologo13.com/wp-content/uploads/2014/12/loopback.jpg" alt="" width="300" height="300" class="aligncenter size-full wp-image-879" />](http://www.gologo13.com/wp-content/uploads/2014/12/loopback.jpg)

[Node.js Advent Calendar 2014](http://qiita.com/advent-calendar/2014/nodejs)の9日目の記事です。 ブログ記事を上げるのが遅くなってすみません。

今回は、Node.jsのWAFである[LoopBack](http://loopback.io/)の使い方について簡単に紹介しようと思います。使ってみた感触としては、ORMがすごく優秀で、RestAPIを自動で生成してくれたりと非常に強力なフレームワークだと感じました！では紹介していきます。

<!--more-->

## loopback とは

loopback とは [StrongLoop](strongloop.com) という mBaaS (Mobile Backend as a Service) を事業としている会社がOSSとして公開しているNode.js の isomorphic な Webフレームワークのことです。

[公式ページ](http://loopback.io/)に書かれている特徴は以下のとおりです。

<pre>LoopBackは高い拡張性があるNode.jsのフレームワークである

- 動的なRestAPIを生成するためにコマンドラインが利用できるよ
- デバイスとブラウザをデータとサービスに接続できる ※iPhone SDK, Android SDKがあるのでアプリ開発にも使えます
- プッシュ通知、ファイル管理、サードパーティログイン、位置情報と連携できる
- オンプレミス（自社サーバ）でもクラウドでも使えます
- StrongLoop Studio API Composer を使えば、LoopBackアプリを見た目で操作できるよ
- APIをセキュアに管理するために、Loopback API gateway をAPIクライアントとPIサーバの中継サーバとして使えます
</pre>

## インストール

まずは generator-loopback をインストールします。 プロジェクトのディレクトリを作成後に、yo で loopback の雛形を生成します。

<pre>$ npm i -g generator-loopback
$ mkdir sample &#038;&#038; cd sample
$ yo loopback
</pre>

## loopback のディレクトリ構成、ファイル説明

yo で雛形を生成すると、以下のようなディレクトリ構成になっています。

<pre>.
├── client
│   └── README.md
├── package.json
└── server
  ├── boot
  │   ├── authentication.js
  │   ├── explorer.js
  │   ├── rest-api.js
  │   └── root.js
  ├── config.json        ... RestAPIに関する設定（ホスト名、ポート番号を記述）
  ├── datasources.json   ... データベースに関する設定（DB名、ホスト名などを記述）
  ├── model-config.json  ... モデル管理設定
  └── server.js          ... loopbackの本体ファイル
</pre>

server/server.js の中身を見てみれば、`app.use(loopback.favicon());`といったコードがあります。[express](http://expressjs.com/)と似てますが、実はloopbackはexpressを内部で利用しているフレームワークなのです。

## モデル

loopbackにおいてモデルは非常に重要で、モデルはデータベースに対するORMです。loopbackのモデルは、MongoBD, MySQL, Oracleといったデータベース製品を抽象化できます（後述）。

loopbackのすごい点は、**モデルを作るだけでRest APIも生成される**という点です。経験的にWebAPIの開発において、DBモデルを作ったあとはそれを操作するためのAPI(GET, POST, PUT, DELETE)などを作成しますよね。こういったルーチンワークが自動化されるというのは本当に素晴らしいことだと思います。

では、以下では実際にモデルを作ってみます。ちなみに、[Users](http://docs.strongloop.com/display/public/LB/Using+built-in+models)というモデルは事前に定義されています。

まず、Bookmark という名前のモデルを作成します。 `yo loopback:model` を実行するとインタラクティブなシェル上が立ち上がり、モデルの情報の入力が促されます。 以下の例では、`title`プロパティと`url`プロパティを追加しています。

<pre>$ yo loopback:model Bookmark
? Enter the model name: Bookmark （&lt;-モデル名）
? Select the data-source to attach Bookmark to: db (memory)　（&lt;-データの保存場所）
? Select model's base class: PersistedModel　（&lt;-モデルの継承クラス）
? Expose Bookmark via the REST API? Yes　（&lt;-モデルをRestAPIとして公開するか？）
? Custom plural form (used to build REST URL):
Let's add some Bookmark properties now.

Enter an empty property name when done.
? Property name: title
invoke   loopback:property
? Property type: string
? Required? Yes

Let's add another Bookmark property.
Enter an empty property name when done.
? Property name: url
invoke   loopback:property
? Property type: string
? Required? Yes

Let's add another Bookmark property.
Enter an empty property name when done.
? Property name:
</pre>

１つ選択に迷うポイントとしては、`Select model's base class:` のところで [Model](http://docs.strongloop.com/display/public/LB/Basic+model+object)か[PersistedModel](http://docs.strongloop.com/display/public/LB/PersistedModel+class) のどちらを選ぶべきかというところです。

違いとしては、Modelは[モデルデータの変更や削除があった場合にコールバックを実行する](http://docs.strongloop.com/display/public/LB/Model+hooks)ことができたり、[モデルデータにスキーマ定義に反するデータ型を代入しようとした時に、エラーを発生してくれるvalidation機能](http://docs.strongloop.com/display/public/LB/Validating+model+data)であったりを提供しています。 一方で、PersistedModel は Model を継承したモデルクラスで、Modelで定義されたメソッドに加えて、データベース操作のためのCRUD機能をサポートします。どういったメソッドがあるかは[ここ](http://docs.strongloop.com/display/public/LB/PersistedModel+class)で確認できます。 なので、モデルをデータベースと対応させるなら、**PersistedModel** を選択すればOK。

モデルの説明は以上にして、モデルを生成すると、トップディレクトリに `common` というディレクトリが作成されて、ここにモデルの定義ファイルが２つ配置されます。loopback は isomorphic なフレームワークであるので、LoopbackとAngular.jsと組み合わせ使うときはこのモデルファイルはブラウザJSとサーバサイドJS(node.js)とで共有されます。

<pre>.
├── client
├── package.json
├── server
└── common/
  └── models
    ├── bookmark.js　（&lt;-NEW!)
    └── bookmark.json　（&lt;-NEW!)
</pre>

新しく生成されたファイルの中身を見てみましょう。 bookmark.json はモデルのスキーマ定義です。入力したカラムの情報が定義されてますね。

<pre>$ cat common/models/bookmark.json
{
  "name": "Bookmark",
  "base": "PersistedModel",
  "idInjection": true,
  "properties": {
    "title": {
      "type": "string",
      "required": true
    },
    "url": {
      "type": "string",
      "required": true
    }
  },
  "validations": [],
  "relations": {},
  "acls": [],
  "methods": []
}
</pre>

次に、bookmark.js はモデルの実装ファイルです。この時点では実装がないように見えますが、先ほど紹介したModelであったり、PersistedModelのメソッドを呼び出すことができます。もちろんここに独自のロジックメソッドを追加することも可能です [参考](http://docs.strongloop.com/display/public/LB/Remote+methods)。

<pre>$ cat common/models/bookmark.js
module.exports = function(Bookmark) {

};
</pre>

## Relation

モデルの [Relation](http://docs.strongloop.com/display/public/LB/Creating+model+relations) も yo コマンドで生成することができます。 1対1、1対多、多対多の関係を作ることができます。

先ほど作った Bookmark モデルに加えて、Page モデルがあるとします。 Page は複数の Bookmark を持つことができるとします。 すると、Relation は以下のように作れます。

<pre>$ yo loopback:relation
? Select the model to create the relationship from: Page
? Relation type: has many （&lt;-関係）
? Choose a model to create a relationship with: Bookmark
? Enter the property name for the relation: bookmarks
? Optionally enter a custom foreign key:
? Require a through model? No　（&lt;-交差テーブルを持つかどうか）
</pre>

relationを作ると、PageモデルのJSONスキーマにその関係が追記されます。 また、relationを作ると、`GET /Pages/{id}/bookmarks`といった具合にモデルに紐づくリレーションも考慮して、RestAPIを生成してくれます。すごく気が利いてますね。

<pre>$ cat common/models/page.json
less page.json
{
  "name": "Page",
  "base": "PersistedModel",
  ...(略)...
  "relations": {
    "bookmarks": {
      "type": "hasMany",
      "model": "Bookmark",
      "foreignKey": ""
  }
}
</pre>

## Explorer

](http://docs.strongloop.com/display/public/LB/Use+API+Explorer) について紹介します。モデルを作ると自動でRestAPIが生成されることについて先ほど触れましたが、 explorerは生成されたAPIを一覧化してくれて、ドキュメントとして使えますし、APIの動作確認にも使うことができます。

それではまず Explorer を起動して、ブラウザで `http://0.0.0.0:3000/explorer` を開いてみましょう。

<pre>$ node .
Browse your REST API at http://0.0.0.0:3000/explorer
Web server listening at: http://0.0.0.0:3000/
</pre>

explorerをブラウザで開くと以下の様な画面です。

![](http://www.gologo13.com/wp-content/uploads/2014/12/Screen-Shot-2014-12-09-at-21.26.47.png)

上のスクリーンショット見てもらえればわかるように、Bookmarkデータの登録API(POST /Bookmarks)であったり、Bookmarkデータの一覧取得(GET /Bookmarks)といったAPIが自動で生成されます。

![](http://www.gologo13.com/wp-content/uploads/2014/12/Screen-Shot-2014-12-09-at-21.36.04.png)

リストアップされた個々のAPIをクリックすると、以下のように画面が展開されてここでAPIの動作確認ができます。

## データベース接続

今までモデルのデータストアとしてメモリを選択していましたが、もちろんMongoDBやMySQLといったデータベース製品を選択することができます。 MongoDBをloopbackと一緒に使う場合は、[loopback-connector-mongodb](https://github.com/strongloop/loopback-connector-mongodb)をインストールします。 MySQLだと、[loopback-connector-mysql](http://github.com/strongloop/loopback-connector-mysql)です。 [こちら](http://docs.strongloop.com/display/public/LB/Connecting+models+to+data+sources)にどのデータベース製品が使えるかがリストアップされています。

実際の使い方は[こちら](http://yuumi3.hatenablog.com/entry/2014/10/08/093137) がわかりやすいです！丸投げすみません。

## Loopback with AngularJS

Loopback を AngularJS と一緒に使う場合についてです。端折り気味ですみませんが、[こちらのworkshop](https://gist.github.com/bajtos/7aaf713305060a7ee895)が取っ付きとしてはわかりやすいです。

より詳しい解説としては [AngularJS JavaScript SDK](http://docs.strongloop.com/display/public/LB/AngularJS+JavaScript+SDK) がわかりやすいです。

## もっと学びたい人

まず最初に呼んでほしいのが [LoopBack core concepts](http://docs.strongloop.com/display/public/LB/LoopBack+core+concepts)ですね。あと Loopback には豊富なドキュメントがあるので、是非眺めてみてください！ http://docs.strongloop.com/display/SL/StrongLoop 

## 最後に

Loopbackの使い方について解説していきました。本当はLoopbackを使ってWebアプリケーションを作りたかったのですが、時間がなく間に合いませんでした。。のちほど作ったアプリケーションの紹介を行いたいと思います！