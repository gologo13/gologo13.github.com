---
id: 503
title: GitHub as a Platform
date: 2013-03-09T23:45:19+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=503
permalink: /2013/03/09/github-as-a-platform/
categories:
  - trivial
---
[<img src="http://www.gologo13.com/wp-content/uploads/2013/03/200px-GitHub.png" alt="200px-GitHub" width="200" height="89" class="aligncenter size-full wp-image-512" />](http://www.gologo13.com/wp-content/uploads/2013/03/200px-GitHub.png)

vim のパッケージ管理を pathogen から NeoBundle へと移行している時にふと思ったこと。

私は vim のパッケージ管理として [pathogen](https://github.com/tpope/vim-pathogen) を２年間使ってきた。指定したフォルダの中にパッケージを放り込むと、それを autoload してくれる優れもの。

しかし、最近の主流は [Vundle](http://github.com/gmarik/vundle.git) や [NeoBundle](https://github.com/Shougo/neobundle.vim)。これらは .vimrc に使いたいパッケージを明示的に書く必要があるけど、`:NeoBundleInstall` とか `:NeoBundleInstall!` とかすれば、パッケージがない場合はインストール、パッケージがある場合は更新を検出して、アップデートしてくれる。

つまり、.vimrc ファイルと Vundle or NeoBundle だけあれば、新しい vim 環境を簡単に構築できるという利点がある。

あるパッケージを使いたい場合、.vimrc には次のように書けばいい。

`NeoBundle 'thinca/vim-quickrun'`

これは http://github.com/thinca/vim-quickrun パッケージを利用しますという宣言である。GitHub からソースコードを取ってくるということなのだが、URLではなく、ユーザ名とリポジトリを指定するのである（もちろん、URLも指定可）。

これを見てふと思った。**GitHub はプラットフォームなのだと。**

考えてみると、他のプログラミング言語のパッケージ管理システムもこの書き方と同じだ。

  * node.js: npm
  * Ruby: rubygems
  * etc&#8230;

他にもあるかもしれないけど、GitHub からパッケージのソースコードを取得するのが、当たり前のようになっている。GitHub はただのホスティングサービスの枠を超えて、developer の拠り所なのだ。

将来、新しいプログラミング言語が生まれると、その言語のパッケージ管理システムも開発されるだろう。そして、パッケージの取得先として当たり前のように GitHub が選ばれるのだと思う。

私はこういうサービスを作りたい。