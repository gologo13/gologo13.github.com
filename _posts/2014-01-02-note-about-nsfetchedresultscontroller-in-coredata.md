---
id: 685
title: CoreDataのNSFetchedResultsControllerに関するメモ
date: 2014-01-02T01:48:33+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=685
permalink: /2014/01/02/note-about-nsfetchedresultscontroller-in-coredata/
categories:
  - coredata
  - objective-c
---
**NSFetchedResultsController** の挙動について少しまとめます。
  
UITableView で CoreData のデータを利用するときに使うクラスです。

### 初期化

まず NSFetchedResultsController の初期化方法

<pre class="lang:objc">NSFetchedResultsController *controller = [[NSFetchedResultsController alloc]
        initWithFetchRequest:fetchRequest
        managedObjectContext:context
        sectionNameKeyPath:nil
        cacheName:@“HogeCache”];
</pre>

  * fetchRequest 
      * View に表示するためのデータを取得するための NSFetchRequest を指定
      * NSFetchRequest に NSSortDescriptor は必ず指定しないといけない
  * context 
      * データの取得、変更の監視を行う NSManagedObjectContext を指定
  * sectionNameKeyPath 
      * セクションを指定するときに指定する。
  * cacheName 
      * fetch した結果をディスクにキャッシュするかどうか
      * キャッシュしない場合は、nil を指定

### デリゲートメソッド

UITableView 上でのデータの挿入、更新、削除、移動イベントに対して、何か独自の処理を行いたいときは、NSFetchedResultsController にデリゲートをセットします。

<pre class="lang:objc">controller.delegate = self; // self は NSFetchedResultsControllerDelegate プロトコルに準拠した UITableView クラス
</pre>

NSFetchedResultsController のインスタンスに delegate を指定すると、以下のデリゲートメソッドが呼ばれる。

<pre class="lang:objc">// この３つはセットで使う
– controllerWillChangeContent:
– controller:didChangeObject:atIndexPath:forChangeType:newIndexPath:
– controllerDidChangeContent:

// section 関連
– controller:didChangeSection:atIndex:forChangeType:
– controller:sectionIndexTitleForSectionName:
</pre>

### デリゲートメソッドの実装方法

以下がデリゲートメソッドの実装方法です。ほとんど[Appleのサンプルコード](https://developer.apple.com/library/ios/documentation/CoreData/Reference/NSFetchedResultsControllerDelegate_Protocol/Reference/Reference.html#//apple_ref/occ/intf/NSFetchedResultsControllerDelegate)と同じです。
  
**NSFetchedResultsChangeUpdate の時だけちょっと実装を変えています**（理由は [こちら](http://oleb.net/blog/2013/02/nsfetchedresultscontroller-documentation-bug/)）。
  
例えば、新しいデータがインサートされてきた時に、ダウンロード処理をフックするとか、独自の処理をここに記述できます。

<pre class="lang:objc">- (void)controllerWillChangeContent:(NSFetchedResultsController *)controller
{
    [self.tableView beginUpdates];
}
 
- (void)controller:(NSFetchedResultsController *)controller didChangeObject:(id)anObject
    atIndexPath:(NSIndexPath *)indexPath forChangeType:(NSFetchedResultsChangeType)type
    newIndexPath:(NSIndexPath *)newIndexPath
{
    UITableView *tableView = self.tableView;
 
    switch(type) {
        case NSFetchedResultsChangeInsert:
            [tableView insertRowsAtIndexPaths:@[newIndexPath] withRowAnimation:UITableViewRowAnimationFade];
            break;

        case NSFetchedResultsChangeDelete:
            [tableView deleteRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationFade];
            break;

        case NSFetchedResultsChangeUpdate:
            [tableView reloadRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAutomatic];
            break;

        case NSFetchedResultsChangeMove:
            [tableView deleteRowsAtIndexPaths:@[indexPath]    withRowAnimation:UITableViewRowAnimationFade];
            [tableView insertRowsAtIndexPaths:@[newIndexPath] withRowAnimation:UITableViewRowAnimationFade];
            break;
    }
}

- (void)controllerDidChangeContent:(NSFetchedResultsController *)controller
{
    [self.tableView endUpdates];
}
</pre>

### デリゲートメソッドが呼ばれるタイミング

`controller:didChangeObject:atIndexPath:forChangeType:newIndexPath:` が呼ばれるのは、初期化時に指定した context に**変化**があった時です。変化というのは以下の３種類。

  * NSFetchedResultsChangeInsert 
      * `[NSEntityDescription entityForName:inManagedObjectContext:]` が実行された時
  * NSFetchedResultsChangeUpdate 
      * NSManagedObject のインスタンスに値が代入された時
      * ※インスタンスが保持している値と代入する値が全く同じでも、デリゲートが呼ばれます
      * ※セルにアニメーションを仕込んでいるときは要注意（セルがリロードされて何度もアニメーションが発生してしまうので） </ul> 
      * NSFetchedResultsChangeDelete 
          * `[NSManagedObjectContext deleteObject:]` が実行された時
    
    NSManagedObject の変化がまとめてこのデリゲートメソッドに通知されます(controllerWillChangeContent: と controllerDidChangeContent: が１回呼ばれる間に、 複数 controller:didChangeObject:atIndexPath:forChangeType:newIndexPath: が呼ばれる)。[NSManagedObjectContext save:] を呼び出した時に、**NSManagedObjectContextDidSaveNotification** の通知が飛ばされます。NSFetchedResultsController は内部的にこの通知を購読していて、この通知を受け取った時に、これらのデリゲートメソッドを呼び出しているのではないかと思います。
    
    複数の変化がまとまってやってくるので、**非同期処理**とかここで行う場合は要注意です。
  
    controller:didChangeObject:atIndexPath:forChangeType:newIndexPath: で渡ってくる indexPath のセルと非同期処理のコールバックで戻ってきた時に処理を行うセルがミスマッチしていて、適切に更新できない場合があります。
  
    </p> 
    
    ### キャッシュ
    
    キャッシュを使うかどうかは、NSFetchedResultsController の初期化時点で指定することができます。
  
    キャッシュを使うことで、NSManagedObject と UITableView の indexPath の対応を再計算するコストを回避できます。キャッシュを利用する際の注意点について。私はこのキャッシュについてあまり理解せず使っていて、ちょっとハマりました。。
    
      * 複数の NSFetchedResultsController で同じキャッシュを利用していけない。キャッシュ名はしっかり分ける。
      * NSFetchRequest の predicate や sortDescriptors が変わった場合、fetchedResultsController を呼び出す前に、deleteCacheWithName: を呼び出して、キャッシュをクリアする必要がある。
    ### NSFetchedResultsController v.s. NSFetchRequest
    
    ただ単に CoreData からデータを取得したいだけなら、NSFetchedResultsController を使う必要はないです。
  
    以下のように、NSFetchRequest を使うことで、クエリの実行が可能です。
    
    <pre class="lang:objc">NSFetchReqeust *fetchRequest = [NSFetchRequest fetchRequestWithEntityName:@"hogeEntity];
fetchRequest.predicate = ...;
fetchRequest.sortDescriptors = ...;

NSError *error = nil;
NSArray *results = [context executeFetchRequest:fetchRquest error:&#038;error];
</pre>
    
    ### リンク
    
      * [NSFetchedResultsController Class Reference](https://developer.apple.com/library/ios/documentation/CoreData/Reference/NSFetchedResultsController_Class/Reference/Reference.html#//apple_ref/doc/uid/TP40008227-CH1-SW24)
      * [NSFetchedResultsControllerDelegate Protocol Reference](https://developer.apple.com/library/ios/documentation/CoreData/Reference/NSFetchedResultsControllerDelegate_Protocol/Reference/Reference.html#//apple_ref/occ/intf/NSFetchedResultsControllerDelegate)
      * http://cimgf.s3.amazonaws.com/NSFRC_iPhoneDevCon10.pdf
    <div class="amazlet-box" style="margin-bottom:0px;">
      <div class="amazlet-image" style="float:left;margin:0px 12px 1px 0px;">
        <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798039799/gologo13-22/ref=nosim/" name="amazletlink" target="_blank"><img src="http://www.gologo13.com//HLIC/513NqbpaaXL._SL160_.jpg" alt="iOS Core Data徹底入門" style="border: none;" /></a>
      </div>
      
      <div class="amazlet-info" style="line-height:120%; margin-bottom: 10px">
        <div class="amazlet-name" style="margin-bottom:10px;line-height:120%">
          <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798039799/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">iOS Core Data徹底入門</a> 
          
          <div class="amazlet-powered-date" style="font-size:80%;margin-top:5px;line-height:120%">
            posted with <a href="http://www.amazlet.com/" title="amazlet" target="_blank">amazlet</a> at 14.01.01
          </div>
        </div>
        
        <div class="amazlet-detail">
          國居 貴浩 <br />秀和システム <br />売り上げランキング: 12,185
        </div>
        
        <div class="amazlet-sub-info" style="float: left;">
          <div class="amazlet-link" style="margin-top: 5px">
            <a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798039799/gologo13-22/ref=nosim/" name="amazletlink" target="_blank">Amazon.co.jpで詳細を見る</a>
          </div>
        </div>
      </div>
      
      <div class="amazlet-footer" style="clear: left">
      </div>
    </div>