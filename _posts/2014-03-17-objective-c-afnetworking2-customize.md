---
id: 750
title: ヘッダのカスタマイズや独自処理をしたいときの AFNetworking 2.0 の使い方
date: 2014-03-17T07:48:41+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=750
permalink: /2014/03/17/objective-c-afnetworking2-customize/
categories:
  - ios
  - objective-c
  - OSS
---
ヘッダのカスタマイズや独自処理をしたいときの AFNetworking 2.0 の使い方

# 普通の使い方

`AFHTTPRequestOperationManager` というクラスを主に利用します。 GETで通信したい場合は、以下のように `GET:parameters:success:failure:` メソッドを呼び出すことで、リクエストを開始することができます。 parameters: に NSDictionary 型のデータを渡せば、それをよしなにURIパラメータやBODYに付与してくれます。

サーバとの通信に成功しレスポンスが返って来た場合には、success: で指定したブロックが呼び出されます。また、ネットワークに繋がっていなかったり、指定したURLのサーバホストの名前解決がでいないなどサーバとの通信に失敗した場合は、failure: で指定したブロックが呼び出されます。 ちなみに、`AFHTTPRequestOperation` からステータスコードやレスポンスヘッダといった情報を取り出すことができます。

<pre class="lang:objc">AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
[manager GET:@"https://hogehoge.api.com/user"
  parameters:@{ @"user_id":@"hoge" }
     success:^(AFHTTPRequestOperation *operation, id responseObject) {
         NSLog(@"res:%@", responseObject);
     }
     failure:^(AFHTTPRequestOperation *operation, NSError *error) {
         NSLog(@"error:%@", error);
     }];

</pre>

GET 以外には、POST, DELETE, PUT 用のメソッドも用意されています。

# ヘッダのカスタマイズ

さて、ここからカスタマイズ編です。リクエスト時のヘッダをカスタマイズしたい場合は、以下のように `AFHTTPRequestOperationManager` の `requestSelializer` というプロパティに対して、`setValue:forHTTPHeaderField:` を呼び出します。 `NSMutableURLRequest` にヘッダを設定する場合と似てますね。

<pre>AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
[manager.requestSerializer setValue:@"SomeValue" forHTTPHeaderField:@"SomeHeaderField"]
</pre>

ちなみに、BASIC認証したい場合は、以下のメソッドが使えます。

<pre>- (void)setAuthorizationHeaderFieldWithUsername:(NSString *)username
                                       password:(NSString *)password;

...

[manager.requestSerializer setAuthorizationHeaderFieldWithUsername:@"username"
                                                            password:@"xxx"];

</pre>

# NSURLRequest のカスタマイズ

リクエストを開始する前に`NSURLRequest`にある処理を実行したいという場合があると思います。 例えば、Parse を使っていてリクエストヘッダにアクセストークンを付与したい場合、以下のように行うことができます。

<pre class="lang:objc">AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];

AFHTTPRequestSerializer *selializer = [AFHTTPRequestSerializer serializer];
self.requestSerializer = selializer;

NSString *URLString = @"https://api.twitter.com/1.1/friendships/create.json";

// リクエストに使う NSURLRequest を生成
// このメソッドを使うことで、AFNetworkingのパラメータのエンコードを良しなにやってくれる処理を再利用できる
NSMutableURLRequest *request =
   [selializer requestWithMethod:@"POST"
                       URLString:URLString
                      parameters:@{ @"screen_name":@"gologo13" }
                           error:nil];
    
// 独自の処理 リクエストヘッダに Twitter API を叩くためのアクセストークンを付与する
[[PFTwitterUtils twitter] signRequest:request];

// リクエスト開始
AFHTTPRequestOperation *operation = [self HTTPRequestOperationWithRequest:request success:success failure:failure];
[self.operationQueue addOperation:operation];
</pre>

最初に紹介したやり方よりは記述量が多くなってしまいますが、必ず毎回実行したい処理なら`AFHTTPRequestOperationManager`のカテゴリ拡張もしくはサブクラスを作っても良いかもしれません。

# Reference

  * http://qiita.com/asakahara/items/9cb68bef56ca70b505c6
  * http://qiita.com/jtemplej/items/c3c25a5301c7250305fe 
      * Request Serialization, Response Serialization の説明がわかりやすい