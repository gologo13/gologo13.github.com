---
id: 607
title: vagrant+chef-soloで作るモダンなPHP開発環境構築(serverspecによる自動テスト付き）
date: 2013-07-01T01:45:23+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=607
permalink: /2013/07/01/php-development-environment-with-vagrant-chef-solo-laravel-serverspec/
categories:
  - chef
  - php
  - serverspec
  - vagrant
---
今時のモダンなPHPの開発環境の構築方法について調べてみました。
  
使用するPHPフレームワークとして、2013年注目すべきPHPフレームワークである [Laravel4](http://laravel.com/docs) を採用しました ([出展 &#8211; 2013年において注目すべき PHP フレームワークは Laravel](http://blog.sarabande.jp/post/48522241291))。

### 使用した技術

ざっくり使用した技術の解説

  * Vagrant 
      * 仮想環境を動かすためのフロントエンドツール
  * VirtualBox 
      * 仮想環境を動かすためのバックエンドツール
  * chef-solo 
      * Provisioningツール(環境の設定・準備をする）
  * serverspec 
      * 環境に対してテストを実行するツール

* * *

### さっそく環境構築

以上の技術の設定ファイル等をひと通りまとめたものを以下のリポジトリに push しました。

  
https://github.com/gologo13/vagrant-laravel-starterkit

詳細は [README の Setup の章](https://github.com/gologo13/vagrant-laravel-starterkit/blob/master/README.md) を読んでいただくとして、以下のとおりにコマンドを実行すると環境構築がおおむね完了するはず。

[crayon-51f9568c71205854640965/]

あとは Laravel の作業ディレクトリである sandbox で作業をして、素晴らしいウェブサイトを作るだけです！

sandbox 以下のファイルは仮想環境と同期されています。
  
ですから、ホスト環境でここのファイルを編集して、ブラウザで確認すると即座に変更が反映されます。
  
もちろん、ホスト環境では好きなエディタ、IDEを使用頂けます。

* * *

### TODO

  * アプリケーションパッケージの自動デプロイ設定 
      * capistrano, Fabric 等というツールが使えそう
  * 本番環境向けの chef 設定