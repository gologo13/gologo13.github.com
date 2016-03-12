---
id: 196
title: More Effective C++ 読書メモ2
date: 2012-09-20T02:17:29+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=196
permalink: /2012/09/20/more-effective-c-reading-memo2/
categories:
  - c++
---
本日はリソース管理について学んだ。コンストラクタ中で例外呼ぶなと聞いたことがあったが、部分的にしかコンストラクタが生成されないと、デストラクタが呼ばれないからだったのか。スマートポインタを使えば、メモリリソースの管理がずっと楽になる。可能な限り生ポインタではなく、スマートポインタを使おう。

本では std::auto\_ptr だったが、boost::shared\_ptr の方が良い。

* * *

p.37 &#8211; p.54

  * 配置 new: 既に割り当てられたメモリ領域にコンストラクタをロードする 
      * new 演算子, operator new, 配置 new
  * **例外**

  
      * 9項：リソースリークを防ぐためにデストラクタを使う 
          * スマートポインタを使おう
          * C 風のライブラリでもスマートポインタの実装のようにラップすれば、リソース管理しやすくなる
      * 10項：コンストラクタでのリソースリークを防ぐ（重要） 
          * コンストラクタ中で補足されない例外が起こった場合、デストラクタが呼ばれない
          * try-catch でコンストラクタ中に例外を監視し、発生した場合 delete
          * メンバ変数が const 付きの場合、初期化リスト内で初期化するような private 関数を用意
          * 結局、スマートポインタを使えば、上のような private 関数も必要なく、デストラクタは極めてシンプルになる

<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894714760/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51UonhV7KhL._SL160_.jpg" alt="新訂版 More Effective C++ (AddisonーWesley professional co)" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894714760/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">新訂版 More Effective C++ (AddisonーWesley professional co)</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/browse/ASIN/4894714760/gologo13-22/ref=nosim/" title="新訂版 More Effective C++ (AddisonーWesley professional co)" target="_blank">amazlet</a> at 12.09.20
      </div>
    </div>
    
    <div class="amazlet-detail">
      スコット・メイヤーズ <br />ピアソンエデュケーション <br />売り上げランキング: 259190<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4894714760/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jp で詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>