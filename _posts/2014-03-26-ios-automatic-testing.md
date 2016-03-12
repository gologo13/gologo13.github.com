---
id: 759
title: 「iOSアプリ:テスト自動化入門」が届いた
date: 2014-03-26T02:43:09+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=759
permalink: /2014/03/26/ios-automatic-testing/
categories:
  - ios
  - testing
---

[ <img src="http://www.gologo13.com/wp-content/uploads/2014/03/IMG_4848-225x300.jpg" alt="" width="225" height="300" class="aligncenter size-medium wp-image-760" />](http://www.amazon.co.jp/gp/product/4798040894/ref=as_li_ss_tl?ie=UTF8&camp=247&creative=7399&creativeASIN=4798040894&linkCode=as2&tag=gologo13-22)<img src="http://ir-jp.amazon-adsystem.com/e/ir?t=gologo13-22&#038;l=as2&#038;o=9&#038;a=4798040894" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />

すごく読みたかった本がようやく届いた。

バックエンド系のシステムだと自動テストがあるのは当たり前になってきたけど、まだまだネイティブアプリでは自動テストが書かれていないというのが実情だと思ってる（私もあまり出来ていない）。 テストができていないと、つまらないミスでアプリがクラッシュしてしまい、AppStoreのレビューが荒れて悲惨なことになる。。 かといって、リリース前に毎回手動テストするのもそれはそれでコストなので、そこで**テストの自動化**でしょという話になってくる。

既存のアプリのすべてのコンポーネントに自動テストを一気に用意するのは、大変だと思うけど、テストを書きやすいところから書いていければいいと思う。UIに依存しない部分、APIにリクエストして結果を取得する部分など。 現実問題、UIのテストってやるべきなのかって話もあるからね。

とりあえず目次を貼って終わりにします。

[iOSアプリ テスト自動化入門｜書籍情報｜秀和システム](http://www.shuwasystem.co.jp/products/7980html/4089.html)

<pre class="nums:false lang:default decode:true " >Chapter 1 テスト自動化への取り組み
1.1 テスト自動化とは
1.1.1 テスト自動化の必要性
1.1.2 自動テストと手動テスト
1.1.3 テスト自動化のROI
1.2 テストの種類と自動化のスコープ
1.2.1 テストレベル
1.2.2 テストタイプ
Chapter 2 テストコードの書きかた
2.1 モデルのユニットテストを書く
2.1.1 XCTestの導入
2.1.2 テストクラスの新規作成
2.1.3 テストメソッドの作成
2.1.4 テストの実行
2.1.5 テストメソッドとアサーションの関係
2.1.6 テスタビリティの高い設計
2.2 既存のアプリにテストを追加する
2.2.1 不具合修正の前にテストを書く
2.2.2 タイミング依存の問題に対してテストを書く
2.2.3 テストを書くことが困難な場合
2.3 ユニットテストのテクニック
2.3.1 構造テストと仕様テスト
2.3.2 仕様化テスト
2.3.3 テストファーストとフェイルイット
2.3.4 TDD（テスト駆動開発）
2.3.5 テストダブル
2.3.6 テストコードの保守性とリファクタリング
2.4 iOSアプリのテストTips
2.4.1 テストフィクスチャをファイルでバンドルする
2.4.2 NSUserDefaultsをクリアする
2.4.3 アプリケーションデータを再現してテスト実行する
2.4.4 Core Dataを使用しているアプリのテスト
2.4.5 Core Dataをインメモリストアで使用する
2.4.6 非公開メソッドをテストする
2.4.7 例外発生をテストする
2.4.8 性能テスト（処理時間の測定）
Chapter 3 ユニットテストフレームワーク
3.1 XCTest
3.1.1 既存プロジェクトにXCTestを導入する
3.1.2 テストターゲットの依存関係
3.1.3 XCTestのアサーション
3.1.4 コマンドラインからXCTestを実行する
3.1.5 OCUnitからXCTestへのコンバート
3.2 GHUnit
3.2.1 GHUnitをプロジェクトに導入する
3.2.2 GHUnitのテスト実行
3.2.3 GHUnitのアサーション
3.2.4 非同期処理のテスト
3.2.5 UIViewの表示テスト
3.2.6 コマンドラインからGHUnitを実行する
3.3 Kiwi
3.3.1 Kiwiをプロジェクトに導入する
3.3.2 Spec（仕様）の記述方法
3.3.3 Expectations（期待値の評価）
3.3.4 テストスタブによる間接入力の操作
3.3.5 モックオブジェクトによる間接出力の検証
3.3.6 プロトコルのモックオブジェクト
3.3.7 非同期処理のテスト
Chapter 4 ユニットテストの補助ツール
4.1 OCHamcrest
4.1.1 OCHamcrestをプロジェクトに導入する
4.1.2 OCHamcrestの使いかた
4.2 OCMock
4.2.1 OCMockをプロジェクトに導入する
4.2.2 テストスタブによる間接入力の操作
4.2.3 特殊な間接入力の操作
4.2.4 モックオブジェクトによる間接出力の検証
4.2.5 プロトコルのモックオブジェクト
4.2.6 クラスメソッドの置き換え
4.2.7 Nice Mock, Partial Mock
4.3 OCMockito
4.3.1 OCMockitoをプロジェクトに導入する
4.3.2 テストスタブによる間接入力の操作
4.3.3 モックオブジェクトによる間接出力の検証
4.3.4 プロトコルのモックオブジェクト
4.3.5 OCMockitoでは実現できないこと
4.4 NLTHTTPStubServer
4.4.1 NLTHTTPStubServerをプロジェクトに導入する
4.4.2 NLTHTTPStubServerの使いかた
4.4.3 レスポンス操作のバリエーション
Chapter 5 システムテストの自動化
5.1 システムテスト自動化の予備知識
5.1.1 システムテストの位置付け
5.1.2 Drive,Judge,Report
5.1.3 システムレベルの機能テスト自動化のROI
5.2 UI Automation
5.2.1 UI Automationの使いかた
5.2.2 テストスクリプトの記述
5.2.3 コマンドラインからテストを実行する
5.2.4 Tuneup JS
5.3 Frank
5.3.1 Frankをプロジェクトに導入する
5.3.2 cucumberコマンドオプション
5.3.3 フィーチャとステップの記述
5.3.4 Symbioteインスペクトツールの利用
5.4 MonkeyTalk
5.4.1 MonkeyTalkのセットアップ
5.4.2 テスト対象アプリとの接続、キャプチャ＆リプレイ
5.4.3 MonkeyTalkのComponentとAction
5.4.4 MonkeyTalkエージェントのアプリへの組み込み
5.5 その他のテスティングフレームワーク
5.5.1 KIF(Keep It Functional)
5.5.2 Appium
5.5.3 Calabash
5.5.4 Zucchini
Chapter 6 ビルドと配布の自動化
6.1 テスト用のビルドを作る
6.1.1 Target, Configuration, Scheme
6.1.2 xcconfigファイルの利用
6.2 ビルドとテスト実行の自動化
6.2.1 xcodebuild
6.2.2 xctool
6.2.3 バージョン番号、Copyrightの更新を自動化する
6.2.4 ビルドの配布方法
6.3 TestFlightによるビルドの配布
6.3.1 TestFlightの利用登録
6.3.2 Upload API
6.3.3 テスターの登録
Chapter 7 CI （継続的インテグレーション）
7.1 OS X Server/Bots
7.1.1 OS X Serverのインストールと設定
7.1.2 Botsによるビルド実行設定
7.1.3 ビルド結果の確認
7.2 Jenkins
7.2.1 Jenkinsのインストールと設定
7.2.2 ジョブの設定
7.2.3 ビルド結果の確認
7.2.4 xctoolによるテスト実行とレポート
7.3 Travis CI
7.3.1 Travis CIの利用登録
7.3.2 .travis.yml
7.3.3 ビルド結果の確認
Chapter 8 メトリック
8.1 コードカバレッジ
8.1.1 Xcodeによるコードカバレッジの採取
8.1.2 CoverStoryによる表示
8.1.3 Jenkins Coberturaプラグインによる表示
8.1.4 Coverallsを利用する
8.2 静的解析
8.2.1 Analyzeビルドアクション
8.2.2 OCLintによる解析
8.2.3 OCLintをJenkinsで実行する</pre>