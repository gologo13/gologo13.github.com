---
id: 547
title: 書評：『UMLモデリングのエッセンス』
date: 2013-04-05T02:39:06+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=547
permalink: /2013/04/05/book-uml-modeling-essence/
categories:
  - book
tags:
  - book
  - OOP
  - software-design
  - uml
---
<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798107956/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/51P6D4Q7T8L._SL160_.jpg" alt="UML モデリングのエッセンス 第3版 (Object Oriented SELECTION)" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798107956/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">UML モデリングのエッセンス 第3版 (Object Oriented SELECTION)</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 13.04.04
      </div>
    </div>
    
    <div class="amazlet-detail">
      マーチン・ファウラー <br />翔泳社 <br />売り上げランキング: 80,601<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798107956/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>

　　

## 感想

ソフトウェア設計に興味があって、読んでみました。198ページで薄い本でしたが、内容は濃くしっかり学べました。 では、感想を書いていきます。

### UML

UML の中で何が重要かと聞かれれば、間違いなく**クラス図**と**シーケンス図**ですね。その証拠にこの本でも、記述の大半はこの２つのダイアグラムに割かれています。この２つに関してはしっかり書かれているので、リファレンスとしても使えると思います。

この2つ以外に使うとすれば、ユースケース図、状態図、配置図、アクティビティ図ぐらいでしょうか。ユースケース図は、ユーザとシステムとのインタラクションについて記述し、状態図はシステムの内部的な状態の遷移を表現する図ですね。また、配置図とアクティビティ図はあまり聞きなれないかもしれませんが、それぞれシステム構成図、フローチャートのようなものです。普段UMLと意識せずに、使っている方もいるかもしれません。

UMLは Unified Modeling Language の略で、グラフィカルなモデリング言語という位置付けになります。言語ですから、当然構文や文法といった仕様がきちんと定義されています。

仕様に従うに越したことはないかもしれませんが、仕様に拘って専門的になりすぎると、逆にUMLの意図が伝わらないかもしれません。結局、クライアントやチームの人たちにその設計の意味が伝わればいいわけです。ですから、自分が描いているイメージを無理やりUMLのいずれかに落としこむよりは、そのチーム内で通じる「名も無きダイアグラム」の方が伝わりやすいかもしれません。それなら後者のダイアグラムを設計図として採用した方が良いということですね。まあ当たり前かもしれません。

他にも、こんなUMLあるよという紹介だけします。

  * アクティビティ図：手続き的なまたは平行な振る舞い
  * シーケンス図：オブジェクト間の相互作用（シーケンスを重視）
  * タイミング図：オブジェクト間の相互作用（タイミングを重視）
  * コミュニケーション図：オブジェクト間の相互作用（リンクを重視）
  * 相互作用図：シーケンス図とアクティビティ図を合わせたもの
  * オブジェクト図：インスタンスの接続の基本例
  * パッケージ図：コンパイル次の階層構造
  * 配置図：ノードへの成果物の配置
  * ユースケース図：ユーザがシステムとどう対話（相互作用）するか
  * 状態図：オブジェクトの存在期間にイベントがオブジェクトに加える変更の内容
  * コンポジット図：クラスのランタイム分割

### オブジェクト指向

また、この本の面白いところは、オブジェクト指向の重要な哲学についても言及されている点です。

オブジェクト指向における重要な考え方である

  * リスコフの置換原則
  * コマンド・クエリ分離原則
  * 契約による設計

などについて学ぶことができます。また、他にも「なぜインタフェースクラスが必要なのか」、「（C++でいうところの）テンプレートクラスと派生クラスの違い」、「依存関係が少ない設計方法」など、ただただUMLの仕様についてだらだらと記述する本とは異なる楽しさがあります。

### 開発プロセス

ソフトウェア開発プロセスについても言及されているのが面白かったです。

ウォータフォール型開発プロセス、反復型開発プロセス、段階的リリースそしてアジャイル開発プロセス。それぞれの長所短所について述べ、最終的には変更に強い反復型開発プロセスまたはアジャイル開発プロセスで開発を行うのがよいと結論付けていました。

## ツール

これは本に書いてなかったことですが、「じゃあ実際にどうやってUMLを書けばいいの？」と思われる方もいると思うので、ここでは UML を作成するツールについて紹介します。もちろん、手書き派の方もそちらでOKだと思います。

### デスクトップ

[<img src="http://www.gologo13.com/wp-content/uploads/2013/04/astah_community_rectangle.png" alt="astah_community_rectangle" width="229" height="66" class="aligncenter size-full wp-image-559" />](http://astah.change-vision.com/ja/product/astah-community.html)

デスクトップで使える、おすすめの UML 作成ツールは [astah* community](http://astah.change-vision.com/ja/product/astah-community.html) 一択という感じでしょうか。無料で、使いやすくて、非の打ち所がないです。 Windows版、Mac版、Linux版とマルチプラットフォームにバイナリが用意されているのも魅力的ですね。

私自身、今デザインパターンの勉強をしているのですが、コードだけでなく、astah* を使って UML も合わせて書くようにしています。 → https://github.com/gologo13/design-pattern-practice

この勉強法だと、デザインパターンだけでなく、UMLも一緒に学べて一石二鳥ですね。

### iOS アプリ

なんと astah にiOS版もあります。iPad さえあれば、いつでもどこでも UML が書けますね。

ダウンロードリンクはこちら

<a href="http://click.linksynergy.com/fs-bin/stat?id=ZPtDxHkLFA4&#038;offerid=94348&#038;type=3&#038;subid=0&#038;tmpid=2192&#038;RD_PARM1=https%253A%252F%252Fitunes.apple.com%252Fjp%252Fapp%252Fastah*-uml-pad%252Fid409312603%253Fmt%253D8%2526uo%253D4%2526partnerId%253D30" target="itunes_store"><img src="http://www.gologo13.com//HLIC/badge_appstore-lrg.gif" alt="astah* UML pad - Change Vision, Inc." style="border: 0;" /></a>

### Web

Web版だと、最近見つけた [js-sequence-diagrams by bramp](http://bramp.github.com/js-sequence-diagrams/) になります。 テキストから手書き風のUMLを生成してくれます。

# 参考書籍

最後に、この本で参考文献として挙げられていた書籍に関して紹介します。

<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894713861/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/51QGXG52GCL._SL160_.jpg" alt="実践UML―パターンによる統一プロセスガイド" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894713861/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">実践UML―パターンによる統一プロセスガイド</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 13.04.03
      </div>
    </div>
    
    <div class="amazlet-detail">
      クレーグ ラーマン <br />ピアソンエデュケーション <br />売り上げランキング: 108,548<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894713861/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>

オブジェクト指向についてわかりやすく解説されています

<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4797347783/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/51-dAD2L2gL._SL160_.jpg" alt="アジャイルソフトウェア開発の奥義 第2版 オブジェクト指向開発の神髄と匠の技" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4797347783/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">アジャイルソフトウェア開発の奥義 第2版 オブジェクト指向開発の神髄と匠の技</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 13.04.03
      </div>
    </div>
    
    <div class="amazlet-detail">
      ロバート・C・マーチン <br />ソフトバンククリエイティブ <br />売り上げランキング: 140,808<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4797347783/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>

オブジェクト指向設計やデザインパターンに関して、深く解説している書籍です。私も是非読みたいです。

<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894712679/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/51EJ928HZ3L._SL160_.jpg" alt="UMLリファレンスマニュアル (Object Technology Series)" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894712679/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">UMLリファレンスマニュアル (Object Technology Series)</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 13.04.03
      </div>
    </div>
    
    <div class="amazlet-detail">
      ジェームズ ランボー グラディ ブーチ イヴァー ヤコブソン <br />ピアソンエデュケーション <br />売り上げランキング: 302,753<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894712679/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>