---
id: 477
title: コマンドラインでMIMEヘッダーをエンコード＆デコードする方法
date: 2013-02-23T17:30:43+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=477
permalink: /2013/02/23/commandline-encode-and-decode-mime-header/
categories:
  - Uncategorized
---
## 背景

MIME(マイム)とはインターネットの電子メールで様々なフォーマットを扱えるようにする規格のことです。MIMEによって電子メールにPDF、画像、動画など様々なドキュメントを添付することができます。

しかし、本来電子メールはUS-ASCIIしか使用できないため、メールのヘッダー部分にマルチバイト文字をそのまま入れることはできません。そのため、現在の電子メールでは以下のような形式でエンコードして、ヘッダーに格納しています。

> =?charset?encoding?encoded-text=?=

そこで、このようなフォーマットの文字列をコマンドラインでエンコード、デコードする方法について書いていきます。

こういうときに、nkf コマンドが大活躍します。

なお、MIME の説明については端折るのであしからず。

## インストール

mac の場合

<pre class="brush: shell">$ brew install nkf
</pre>

## 文字エンコーディングの変換

MIMEの前に文字エンコーディングの変換について

  * nkf -w: UTF-8 に変換
  * nkf -e: EUC-JP に変換
  * nkf -s: Shift-JIS に変換
  * nkf -j: JIS(ISO-2022-JP) に変換

## MIMEエンコード 

MIME エンコードは「普通の文字列」を「=?charset?encoding?encoded-text=?=」のような形式の文字列に変換する操作のことです。

### UTF8文字列 → MIME エンコード

「ほげほげ」は UTF8 文字列として、UTF8のままMIMEエンコードするとします。

#### 例

<pre class="brush: shell">$ echo ほげほげ | nkf -M
=?UTF-8?B?44G744GS44G744GS?=

$ echo ほげほげ | nkf -MB
44G744GS44G744GSCg==

$ echo ほげほげ | nkf -MQ
=E3=81=BB=E3=81=92=E3=81=BB=E3=81=92
</pre>

#### 解説

  * nkf -M: Base64 で MIMEエンコードする
  * nkf -MB: Base64 で MIMEエンコードする 
      * encoded text だけ取り出す 
  * nkf -MQ: quoted-printable で MIMEエンコードする 
      * encoded text だけ取り出す 

### UTF8文字列 → MIME エンコード(JIS)

次に、出力のエンコーディングをJISでMIMEエンコードします。 JIS(ISO-2022-JP) は 7bit で表現される文字セットを使用しており、メールのエンコーディング形式として今でもよく使われています。

JIS への変換は、上で説明した通り、nkf -j オプションを加えるだけで簡単に実現出来ます。

#### 例

<pre class="brush: shell">$ echo ほげほげ | nkf -jM
=?ISO-2022-JP?B?GyRCJFskMiRbJDIbKEI=?=

$ echo ほげほげ | nkf -jMB
GyRCJFskMiRbJDIbKEIK

$ echo ほげほげ | nkf -jMQ
=1B=24B=24=5B=242=24=5B=242=1B=28B
</pre>

## MIMEデコード

MIME デコードは「=?charset?encoding?encoded-text=?=」のような形式の文字列を「普通の文字列」に変換する操作のことです。

### 例

<pre class="brush: shell">$ echo "=?ISO-2022-JP?B?GyRCJFskMiRbJDIbKEI=?=" | nkf -w
ほげほげ

$ echo GyRCJFskMiRbJDIbKEI= | nkf -wmB  
ほげほげ

$ echo "=1B=24B=24=5B=242=24=5B=242=1B=28B" | nkf -wmQ
ほげほげ
</pre>

### 解説

nkf -m: MIME デコードする

入力が「=?charset?encoding?encoded-text=?=」の形式の場合、-m オプションなしでも自動でMIMEデコードしてくれます。便利ですね！

入力が encoded-text だけの場合、明示的に -m オプションと content-transfer-encoding の形式を指定します。

# まとめ

nkf コマンドを使って、MIMEエンコード＆デコードしました。 簡単ですね！

# 参考図書

<div class="amazlet-box" style="margin-bottom:0px;">
  <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
    <a href="http://www.amazon.co.jp/exec/obidos/ASIN/477414164X/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/51b7R1hZL-L._SL160_.jpg" alt="プログラマのための文字コード技術入門 (WEB+DB PRESS plus) (WEB+DB PRESS plusシリーズ)" style="border: none;" /></a>
  </div>
  
  <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
    <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
      <a href="http://www.amazon.co.jp/exec/obidos/ASIN/477414164X/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">プログラマのための文字コード技術入門 (WEB+DB PRESS plus) (WEB+DB PRESS plusシリーズ)</a>
      
      <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
        posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 13.02.23
      </div>
    </div>
    
    <div class="amazlet-detail">
      矢野 啓介 <br />技術評論社 <br />売り上げランキング: 128,811<br />
    </div>
    
    <div class="amazlet-sub-info" style="float: left;">
      <div class="amazlet-link" style="margin-top: 5px">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/477414164X/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
      </div>
    </div>
  </div>
  
  <div class="amazlet-footer" style="clear: left">
  </div>
</div>