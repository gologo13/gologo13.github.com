---
id: 23
title: VPS 移転
date: 2012-08-17T00:27:00+00:00
author: yohei
layout: post
guid: http://49.212.183.191/?p=23
permalink: /2012/08/17/moved-from-slicehost-to-sakura/
image:
  - 
seo_follow:
  - 'false'
seo_noindex:
  - 'false'
categories:
  - VPS
tags:
  - VPS
---
[<img class="aligncenter size-medium wp-image-263" title="Logo_lockup_version-2 SPOT" src="http://www.gologo13.com/wp-content/uploads/2012/08/rackspace-300x116.jpg" alt="" width="300" height="116" />](http://www.gologo13.com/wp-content/uploads/2012/08/rackspace.jpg) &nbsp; slicehost(Rackspace) で VPS を借りていたが、さくらの VPS に乗り換えた。 毎月の値段はほとんど変わらないけど、サーバスペックが全然違う。それに、SSH した時のレスポンスも体感的に速い。やはり、データセンターが日本にあるかどうかって意外と大きいのだろうか。ターンアラウンドタイムが 50 ms ~ 100ms ぐらい違うと思う。スペック表は次の通り。 

<table>
  <tr>
    <th>
      VPS
    </th>
    
    <th>
      slicehost
    </th>
    
    <th>
      sakura
    </th>
  </tr>
  
  <tr>
    <td>
      コア数
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
  </tr>
  
  <tr>
    <td>
      メモリ
    </td>
    
    <td>
      256 MB
    </td>
    
    <td>
      1GB
    </td>
  </tr>
  
  <tr>
    <td>
      ディスク容量
    </td>
    
    <td>
      10 GB
    </td>
    
    <td>
      100GB
    </td>
  </tr>
  
  <tr>
    <td>
      月額料金
    </td>
    
    <td>
      870円
    </td>
    
    <td>
      980円
    </td>
  </tr>
  
  <tr>
    <td>
      年間料金
    </td>
    
    <td>
      10,440円
    </td>
    
    <td>
      10,780円(一括の場合)
    </td>
  </tr>
</table> 厳密には slicehost の月額料金はデータの入力量、出力量に比例する。それほどアクセスなかったので、この価格に収まったのかもしれない。 コンテンツを徐々に移していきたい。あと、ブログエンジンも 

[Chyrp](http://chyrp.net/) から WordPress に変更した。Chyrp はシンプルでいいと思って使ったが、あまりカスタマイズ性がなくて、飽きてきた。とりあえずこれからサーバーどんどんいじる！ 

### links {#hs_34e3354dccce2541722f698af32de2a7_header_0}

  * [Cloud Servers Pricing by Rackspace Cloud Computing & Hosting](http://www.rackspace.com/cloud/public/servers/pricing/)
  * [サービス仕様 | VPS（仮想専用サーバ）は「さくらのVPS」](http://vps.sakura.ad.jp/specification.html)