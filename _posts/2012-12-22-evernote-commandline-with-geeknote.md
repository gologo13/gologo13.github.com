---
id: 310
title: コマンドラインからEvernoteを簡単に操作できる！Geeknoteでギークになろう。
date: 2012-12-22T16:27:44+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=310
permalink: /2012/12/22/evernote-commandline-with-geeknote/
categories:
  - lifehack
---
[<img src="http://www.gologo13.com/wp-content/uploads/2012/12/geeknote.png" alt="" title="geeknote" width="282" height="77" class="aligncenter size-full wp-image-312" />](http://www.gologo13.com/wp-content/uploads/2012/12/geeknote.png)

# はじめに

みなさん、[Evernote](http://www.evernote.com/) 使ってますか？すごく便利ですよね。私は読み終わったウェブページ、メモ、写真など何でもEvernoteに放り込んでいます。デバイスを選ばないのも魅力的ですね。

でも、ブラウザで Evernote を開くとめちゃくちゃ重いですよね。ノートの数に比例して重くなるのでしょうか。また、[WYSIWYG](http://ja.wikipedia.org/wiki/WYSIWYG "WYSIWYG - Wikipedia") ライクなエディタも使い心地がイマイチです。 重いと使う気が失せますね。

そこで**コマンドライン**上で Evernote を操作できないかなーと思っちゃうのがギークってやつです。コマンドライン上なら好きなエディタで編集も出来ますね。それが探したら、ありました。

そう、

#### [Geeknote](http://geeknote.me/)

ならね。 オッサンなアイコンで一見ダサいですが、なかなかできるやつです。

# Geeknote

Geeknote のインストール方法と使い方を紹介していきたいと思います。

## インストール

[Geeknote &#8211; how to install](http://www.geeknote.me/install/ "Geeknote - how to install") に書いてあるとおりですが、git clone して、geeknote.py を PATH が通っているディレクトリに置くだけです。

<pre class="brush: shell">$ git clone git://github.com/VitaliyRodnenko/geeknote.git

$ cd geeknote

# Launch Geeknote and go through login procedure.
$ python geeknote.py login
</pre>

Ubuntu/Debian ユーザ用に deb パッケージも用意されていますが、若干古いのでこちらのほうがいいです。

## 使い方

### ログイン

まずログインします。IDとパスワードを入力します。

<pre class="brush: shell">$ geeknote login
Login: xxxxxx                           
Password: 
You have successfully logged in.  
</pre>

### 設定

settings サブコマンドで色々設定ができるそうです。 まだ、editorしか設定項目が無いですが。

<pre class="brush: shell">$ geeknote settings --editor vim
Changes have been saved. 
$ geeknote settings --editor
 Current editor is: vim                  
</pre>

### 投稿

create サブコマンドでメモを投稿できます。 もちろんオプションで投稿するノートブック、タグも指定できます。

標準入力からの投稿もサポートしているようです。cool ですね！(でも時々失敗します）

<pre class="brush: shell">$ geeknote create --title "タイトル" --content "内容"
Note has been successfully created.     

$ echo "内容２" | geeknote create --title "タイトル２"
Note has been successfully created.     
</pre>

　 　

応用として、makrdown 形式でファイルを書いたメモを HTML として投稿出来たりもします。

markdown 形式のファイルを HTML に変換するには、 [ここ](http://daringfireball.net/projects/markdown/ "Daring Fireball: Markdown") から Markdown.pl をダウンロードしてください。

<pre class="brush: shell">$ cat item.markdown
# タイトル

- アイテム1
- アイテム2

$ Markdown.pl &lt; item.markdown | geeknote --title "Makrdownから投稿"
</pre>

### 閲覧、検索

ノートの閲覧は show サブコマンドを使うことで可能です。

使い方としては、show サブコマンドの引数に検索クエリを与え、検索結果の中から目的のノートを選びます。検索結果から目的のノートを選ぶには、先頭についている数字を入力します。

この検索はノートの本文ではなく、タイトルに対して行われます。

<pre class="brush: shell">$ geeknote show "iphone"
Total found: 20                          
  1 : 28.10.2012  i-FunBox | File Manager and Hi-Speed Transfer Tool for iPhone and iPhone 3G (iFunBox Download Page)
  2 : 03.01.2012  毎日日記がつけれそうなiPhoneアプリ Momento | favLife with iPhone
  3 : 20.01.2012  Weblioに登録した単語を簡単にiPhoneで: 綿柿
...
 20 : 24.08.2012  Titanium Mobileで作る！ iPhone／Androidアプリ：第8回　加速センサの使用と実機への転送｜gihyo.jp … 技術評論社
  0 : -Cancel-
 2
</pre>

show サブコマンド自体では、全文検索はできませんが、find サブコマンドと組み合わせることで**全文検索**が可能となります。

<pre class="brush: shell">$ geeknote find "iphone" --content-search      
Search request: iphone                  
Total found: 20
  1 : 28.10.2012  i-FunBox | File Manager and Hi-Speed Transfer Tool for iPhone and iPhone 3G (iFunBox Download Page)
  2 : 19.06.2012  ”あと30分飲みたい”から生まれた「終電後検索」～乗換案内アプリのウラ事情～【ヤフー株式会社のiPhone事情】 - AppBank
  3 : 18.08.2012  Use Appcelerator Titanium to build mobile apps for iPhone &#038; Android and desktop apps for Windows, Mac OS X &#038; Linux from Web technologies
  4 : 10.09.2012  家計簿つけるならZaimとOCN家計簿の組み合わせが最強かも - PR - - nanapi Web
...
 20 : 27.03.2012  海外で言葉がわからなくても会話できる無料iPhoneアプリ「世界会話手帳」 -INTERNET Watch
</pre>

### 編集

なんと編集もできます。edit サブコマンドを使えば。

note オプションで引数を指定すると、その引数を含んだタイトルのノートを検索してくれます。 UI としては geeknote show と同じですね。 ノートを選ぶと、geeknote settings --editor で指定したエディタが開きます（デフォルト：nano）。

<pre class="brush: shell">$ geeknote edit --note "iphone"
  1 : 28.10.2012  i-FunBox | File Manager and Hi-Speed Transfer Tool for iPhone and iPhone 3G (iFunBox Download Page)
  2 : 03.01.2012  毎日日記がつけれそうなiPhoneアプリ Momento | favLife with iPhone
  3 : 20.01.2012  Weblioに登録した単語を簡単にiPhoneで: 綿柿
...
 20 : 24.08.2012  Titanium Mobileで作る！ iPhone／Androidアプリ：第8回　加速センサの使用と実機への転送｜gihyo.jp … 技術評論社
  0 : -Cancel-
1 
</pre>

### その他

全ては紹介できませんが、他の機能として

  * [同期](http://www.geeknote.me/documentation/#gnsync-synchronization-app "Geeknote - documentation")
  * ノートブックの一覧表示
  * ノートブックの作成
  * タグ一覧表示
  * タグの作成
  * タグのリネーム

があるそうです。 詳細は [Geeknote - documentation](http://www.geeknote.me/documentation/ "Geeknote - documentation") をご覧ください。

# まとめ

Geeknote について紹介しました。 ノートの検索、閲覧、投稿、編集、削除、さらに同期などひと通り必要な機能は備えているようです。

ただ、難点を一つ述べると、実行が遅いです。

それでも、CUI 派のあなたならコマンドラインから Evernote を操作できるという魅力を十分感じたはず。