---
id: 791
title: passport-yj 1.0.5 released
date: 2014-05-12T01:50:08+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=791
permalink: /2014/05/12/passport-yj-1-0-5-released/
categories:
  - node.js
  - oauth
  - OSS
---
Yahoo!JAPANのOAuth認証(YConnect)を簡単に行うためのnpm packageである [passport-yj](https://github.com/Lewuathe/passport-yj) に pull request が来ていた。 依存モジュールである [oauth2](https://github.com/ciaranj/node-oauth) のソースコードの中身が変わっていたのか、install後に実行されるパッチが期待通りに適用されていなかった。 動作確認も問題なかったのでマージ。

あと動作確認したときに、同梱しているサンプルで正常にユーザ情報を表示できていなかったので、それも合わせて修正。 どうやらYConnect の userinfo API のレスポンス仕様が変わっていることに気づいた。

作ってから１年も経つと、ライブラリのバージョンが上がったりして思わぬところで問題が起こるのだな。

[passport-yj 1.0.5](https://www.npmjs.org/package/passport-yj)