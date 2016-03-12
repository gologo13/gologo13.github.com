---
id: 709
title: WordPressに全件表示のアーカイブを作る方法（はてブ数表示付き）
date: 2014-01-03T01:00:44+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=709
permalink: /2014/01/03/wordpress-archive/
categories:
  - Uncategorized
---
この WordPress で作ったブログにアーカイブを作ってみました。

[archive](http://www.gologo13.com/archive/)

### 設置方法

アーカイブ表示用のPHPスクリプトを設置する方法については [WordPressで過去記事一覧(アーカイブ)を作成する](http://g86.dbcls.jp/~yag/wordpress/archives/1471) を御覧ください。

全く同じだと芸がないので、別方法でアーカイブを実装してみました。`wp_get_archives` という WordPress にアーカイブ取得専用の関数があるのですが、カスタマイズ性に乏しいためです。

今回の実装では、アーカイブに「日付＋タイトル＋はてブ数」を表示してみました。

実装で、`query_posts()`というブログエントリを取得する関数を使用しました。引数に showposts を指定することで取得するエントリ数を制御できます。私の場合、全件取得したかったので、`query_posts('showposts=-1')` としました。

### PHP Script

<pre class="lang:html"><?php 
/*
Template Name: archive_list // ←　このコメントを削除すると動きません
*/
?>


<?php get_header() ?>



<div id="container">
  <div id="content">
    <div class="entry-content">
      <?php the_content() ?>
      
              
      
      <ul>
        &lt;!— エントリを全件取得する —>
                <?php query_posts('showposts=-1'); ?>
                
        
        <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
                
        
        <li>
          &lt;!— 日付、タイトル —>
                      <span><?php the_date(); ?></span>
          
          <?php echo "<br/>" ?>
                      &nbsp;&nbsp;&nbsp;&nbsp;
          
          <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
          
                     &lt;!— はてブ数を表示する —>
                     
          
          <a href="<?php echo 'http://b.hatena.ne.jp/entry/' . get_permalink(); ?>"><img src="<?php echo 'http://b.hatena.ne.jp/entry/image/' . get_permalink(); ?>" /></a>
                 
        </li>
        
               
        <?php endwhile; endif; ?>
               
      </ul>
      
             
    </div>
        
  </div>
  
  <!-- #content -->
  
</div>

<!-- #container -->



<?php get_footer() ?>
</pre>

### Link

  * [WordPress › フォーラム » 最新の記事タイトル+日付+表示数指定](http://ja.forums.wordpress.org/topic/1009)
  * [WordPress › Support » Show all posts using query_posts? I was so close, but now I&#8217;m stuck..](http://wordpress.org/support/topic/show-all-posts-using-query_posts-i-was-so-close-but-now-im-stuck)
  * [テンプレートタグ/wp get archives &#8211; WordPress Codex 日本語版](http://wpdocs.sourceforge.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/wp_get_archives)