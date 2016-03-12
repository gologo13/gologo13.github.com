---
id: 165
title: C++ で Bloom Filter を実装してみた
date: 2012-09-03T00:13:15+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=165
permalink: /2012/09/03/bloom-filter-implemented-in-c/
categories:
  - algorithm-and-data-structure
---
Bloom Filter を勉強する機会があったので、実装してみた。

## 概要

[Bloom Filter](http://ja.wikipedia.org/wiki/%E3%83%96%E3%83%AB%E3%83%BC%E3%83%A0%E3%83%95%E3%82%A3%E3%83%AB%E3%82%BF "ブルームフィルタ - Wikipedia") 自体の説明はよそに譲るとして、ざっくり特徴を言うと、

  * 二分木やハッシュテーブル等のデータ構造と比べると、はるかにメモリ効率が良い 
      * キーの値をメモリ上で格納する必要がない
      * 逆に言うと、キーの集合を復元できない
  * false positive(追加していないキーに対して true と返す誤り)による誤検出の可能性があるが、false negative(追加しているキーに対して、false と返す誤り)はない 
      * false positive する確率は _1 &#8211; exp(- k \* n / m)) \* k_ の式から算出できる 
          * パラメータ k: ハッシュ関数の個数、n: 追加する要素数, m: ビット列の長さ
          * 要素を追加するほど、false positive が起きやすい 
              * n = 10 のとき 0.028, n = 100 のとき 0.254, n = 1000 のとき 0.947

# Bloom Filter

## コード

<pre class="brush: c++">#include &lt;iostream>
#include &lt;vector>
#include &lt;bitset>
using namespace std;

// ビット列の長さ
static const int kNumBits                   = 1 &lt;&lt; 10;
// ハッシュ関数の個数
static const int kNumHashFuncs              = 3;
// ハッシュ関数の salt
static const unsigned kSalts[kNumHashFuncs] = {137, 69, 545};

/**
 * Bloom Filter
 */
class BloomFilter
{
    bitset&lt;kNumBits> _bs;
    vector&lt;unsigned> genHashes(const string &#038;key);
public:
    /**
     * constructor
     */
    BloomFilter();

    /**
     * 要素を追加する
     */
    void add(const string &#038;key);

    /**
     * 要素の存在をチェックする
     */
    bool exist(const string &#038;key);
};

BloomFilter::BloomFilter()
{
    _bs.reset();
}

vector&lt;unsigned> BloomFilter::genHashes(const string &#038;key)
{
    vector&lt;unsigned> hashes(kNumHashFuncs, 0);
    for (size_t i = 0; i &lt; key.size(); ++i) {
        for (int j = 0; j &lt; kNumHashFuncs; ++j) {
            hashes[j] = hashes[j] * kSalts[j] + static_cast&lt;unsigned>(key[i]);
        }
    }
    for (int i = 0; i &lt; kNumHashFuncs; ++i) {
        hashes[i] %= kNumBits;
    }
    return hashes;
}

void BloomFilter::add(const string &#038;key)
{
    vector&lt;unsigned> hashes(genHashes(key));
    for (vector&lt;unsigned>::const_iterator it = hashes.begin(); 
            it != hashes.end(); ++it) {
        _bs.set(*it, 1);
    }
}

bool BloomFilter::exist(const string &#038;key)
{
    bool ret = false;

    vector&lt;unsigned> hashes(genHashes(key));
    for (vector&lt;unsigned>::const_iterator it = hashes.begin(); 
            it != hashes.end(); ++it) {
        if (_bs[*it])
            return true;
    }
    return ret;
}

int main()
{
    BloomFilter bf;

    bf.add("hoge");
    bf.add("fuga");

    cout &lt;&lt; (bf.exist("hoge") ? "true" : "false") &lt;&lt; endl;
    cout &lt;&lt; (bf.exist("fuga") ? "true" : "false") &lt;&lt; endl;
    cout &lt;&lt; (bf.exist("kuso") ? "true" : "false") &lt;&lt; endl;

    return 0;
}
</pre>

## 実行例

<pre class="brush: shell">true
true
false
</pre>

## 応用

Bloom Filter の応用をいくつか紹介。

  * 自然言語処理 
      * 言語モデルとしての応用 <http://acl.ldc.upenn.edu/D/D07/D07-1049.pdf>
      * 統計的機械翻訳での応用 <http://acl.ldc.upenn.edu/P/P07/P07-1065.pdf>
  * NoSQL データベース 
      * LSM-Tree における SSTable 中にキーの存在を高速に検索 [要出典]
  * Google 日本語入力(Mozc)の共起辞書 
      * [Bloom filter の気持ち - アスペ日記](http://d.hatena.ne.jp/takeda25/20110509/1304948935 "Bloom filter の気持ち - アスペ日記")

## まとめ

使いドコロが難しそうだけど、false positive が起こっても許容できる状況では威力を発揮しそうですね！

## 参考リンク

  * [乱択アルゴリズム紹介(Bloom Filter) | Preferred Research](http://research.preferred.jp/2011/03/bloom-filter/ "乱択アルゴリズム紹介(Bloom Filter) | Preferred Research")
  * [Bloom filterの説明 — ありえるえりあ](http://dev.ariel-networks.com/column/tech/boom_filter/ "Bloom filterの説明 — ありえるえりあ")
  * [Bloom filterのシンプルな実装 - 西尾泰和のはてなダイアリー](http://d.hatena.ne.jp/nishiohirokazu/20080213/1202912207 "Bloom filterのシンプルな実装 - 西尾泰和のはてなダイアリー")