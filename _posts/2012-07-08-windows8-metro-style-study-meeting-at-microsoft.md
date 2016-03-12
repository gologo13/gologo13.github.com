---
id: 500
title: 【第25回GSGL】Windows8勉強会 JavaScript + HTML によるWindows 8 Metro スタイルアプリ開発に参加してきた
date: 2012-07-08T01:10:13+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=500
permalink: /2012/07/08/windows8-metro-style-study-meeting-at-microsoft/
categories:
  - Uncategorized
---
【第25回GSGL】Windows8勉強会 JavaScript + HTML による[Windows 8 Metro スタイルアプリ開発](http://atnd.org/events/28268) に参加してきました。

JavaScript で開発できる Metro スタイルアプリに興味があって、参加しました。 モバイルアプリが JavaScript で開発できるという意味では、[Titanium Mobile](http://www.appcelerator.com/platform)を連想させますね。

感想としては、Metro は一見今までにない UI で取っつきにくそうという印象でしたが、非常に可能性を感じさせますね。ちなみに、あの @dankogai も[Metro UI を褒めてますね！](http://blog.livedoor.jp/dankogai/archives/51731752.html)早く実機で触ってみたいです！

ちなみに、会場はマイクロソフト品川オフィスでした。 オフィス綺麗！

以下、勉強会のメモ

_講師: 物江 修 さん_

## Blend for Visual Studio

  * ドラッグ＆ドロップでコントローラー追加可能
  * DOM Exploer 
      * どのDOM要素が選ばれているか調べられる
      * Tools: Simulator
  * Visual Studio 
      * [Expression Blend](http://www.microsoft.com/japan/products/expression/products/blend_overview.aspx)

## Windows 8

  * システムのライフタイムを管理できる 
      * ライフタイム：アプリケーションの起動から終了までの期間
      * プロセスの状態遷移： 稼働状態 ←→ サスペンド状態 → 終了状態
  * アプリケーションデータ＆ユーザデータ 
      * Metro App. がアクセスできるデータの範囲は限られている（アクセス制限）

## Metro スタイルアプリの特徴

  * 爽快で滑らかな動き
  * スナップでスケールで美しく
  * タイルでユーザとつながる
  * コントラクト

## Contract

  * ユーザとつながるOS・アプリの取り決めのこと
  * 一般的に実装されるコントラクト
  * 検索、共有、設定、リモート再生、ファイル選択ツール
  * _検索コントラクト_ 
      * 同じ検索キーワードを使って、アプリやブラウザ検索ができる
  * _共有コントラクト_ 
      * アプリケーションデータの共有
      * クリップボードのようなもの
  * _設定コントラクト_ 
      * アプリの設定に
      * コンテキストに応じた一貫性の実現

## Tile

  * アプリの顔
  * アプリの拡張部分として重要 
      * Liveタイルがユーザを惹きつけられるのでオススメ
  * ユーザが興味を持ったコンテンツへのアクセスを用意にするために、セカンダリタイルを活用せよ
  * ピン留め

## サイズ

  * 正方形 OR タイル

## トースト通知

  * 注意喚起、お知らせに使える（Notification）

## クラウドのローミング

  * どのデバイスでも、いつもの設定で操作可能
  * 異なるデバイスの状態や初期設定を同期
  * ユーザがデバイスをまたいで作業を継続できるように、アプリのデータを同期 
      * 設定ファイルなどの、あまりサイズが大きくないファイルに適している

## Windows Push Notification Service

  * push 通知してくれるサービスを無償で利用できる？

## Windows.Devices.Sensors

  * デバイスのセンサーを操作するためのAPI 
      * 現時点では、たかだか3つぐらいのセンサーしか装備していない

## Design

  * immersive: ユーザがコンテンツに没頭することを心がける

## インタラクション

  * アプリバー：アプリの下部分
  * チャーム：
  * flyout 
      * 一時的、または文脈上のちょっとしたUIに

## Windows Store

  * アプリの唯一の入手先
  * 売り上げの8割は開発者がもらう 
      * アプリ内課金は10割開発者

## Windows App Certification Kit Test Results

  * アプリの審査をしてくれる 
      * セキュリティとかMetroスタイルを遵守しているか
  * スタイルを守らないと、審査に通らない

## リソースの場所

  * [monoe&#8217;s blog](http://blogs.msdn.com/b/osamum/archive/2012/05/10/developer-camp-html-javascript.aspx) 
      * 実践編フォローアップ を参照せよ
  * [Facebook : Go Metro](https://www.facebook.com/5Metro)