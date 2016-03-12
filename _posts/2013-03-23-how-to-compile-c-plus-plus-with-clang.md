---
id: 518
title: clangでc++コードをコンパイルする方法(解説付き)
date: 2013-03-23T22:28:22+00:00
author: yohei
layout: post
guid: http://www.gologo13.com/?p=518
permalink: /2013/03/23/how-to-compile-c-plus-plus-with-clang/
categories:
  - c++
---
小ネタです。

以下のようなC++プログラムがあるとします。一見全く問題なさそうです。

<pre class="lang:c++ decode:true " title="main.cpp" >#include &lt;iostream&gt;
using namespace std;

int main (int argc, char *argv[])
{
    cout &lt;&lt; "Hello" &lt;&lt; endl;
    return 0;
}</pre>

しかし、このプログラムを以下のように `clang` コマンドでコンパイルすると、コンパイルエラーになります。（Mac 環境）

<pre class="brush: shell">$ clang main.cpp
Undefined symbols for architecture x86_64:
  "std::ostream::operator&lt;&lt;(std::ostream&#038; (*)(std::ostream&#038;))", referenced from:
      _main in example-YhevQb.o
  "std::ios_base::Init::Init()", referenced from:
      ___cxx_global_var_init in example-YhevQb.o
  "std::ios_base::Init::~Init()", referenced from:
      ___cxx_global_var_init in example-YhevQb.o
  "std::cout", referenced from:
      _main in example-YhevQb.o
  "std::basic_ostream&lt;char, std::char_traits&lt;char> >&#038; std::endl&lt;char, std::char_traits&lt;char> >(std::basic_ostream&lt;char, std::char_traits&lt;char> >&#038;)", referenced from:
      _main in example-YhevQb.o
  "std::basic_ostream&lt;char, std::char_traits&lt;char> >&#038; std::operator&lt;&lt;&lt;std::char_traits&lt;char> >(std::basic_ostream&lt;char, std::char_traits&lt;char> >&#038;, char const*)", referenced from:
      _main in example-YhevQb.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)

</pre>

結論として、`clang++`コマンドを使ってコンパイルするのが正解です。
  
clang++ を使うと、無事コンパイルができました。

<pre class="brush: shell">$ clang++ main.cpp
$

</pre>

　
  
　
  
　

このまま終わるのは腑に落ちないので、もう少し背景を説明します。

clang と clang++ の違いは、ライブラリのリンク時に **C++ のライブラリを呼び出すかどうか**という点です。この違いは clang, clang++ コマンドに -v オプションをつけて呼び出すとわかります。

-v オプションをつけて、リンク部分の出力を取り出すと次のようになるはずです。
  
注目すべき点は、**/usr/bin/ld** というリンクが実行される部分です。

clang の出力

<pre class="brush: shell">"/usr/bin/ld" -demangle -dynamic -arch x86_64 -macosx_version_min 10.8.0 -o a.out 
/var/folders/35/5zrgbbf91rgc3zmb_thc10180000gn/T/example-GH6fnD.o -lSystem
 /usr/bin/../lib/clang/4.1/lib/darwin/libclang_rt.osx.a
...
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)

</pre>

clang++ の出力

<pre class="brush: shell">"/usr/bin/ld" -demangle -dynamic -arch x86_64 -macosx_version_min 10.8.0 -o a.out
 /var/folders/35/5zrgbbf91rgc3zmb_thc10180000gn/T/example-nYU1TM.o -lstdc++ -lSystem
 /usr/bin/../lib/clang/4.1/lib/darwin/libclang_rt.osx.a

</pre>

/usr/bin/ld の行を比較すると、clang++ の出力には **-lstdc++** という C++ のライブラリがリンクされているのがわかります。一方で、clang の方はこのリンクがありません。

だから、C++ 固有の _std::cout,_ _std::ostream::operator<<_ などが undefined symbol （意味：宣言はあるけど、実装がない）となり、コンパイルエラーになることがわかります。