---
layout: post
title: "ホームページ作ってみた　その１"
author: "Bear_0821"
---

興味が沸いたので何も分からないなりにサイトを作ってみました。

# 概要

サイトURL：[https://pages.calc.mie.jp/bear0821/](https://pages.calc.mie.jp/bear0821/)

見ればわかりますが基本的な部分しか触っていません。

他サイトのURLの貼り方や文字色・サイズ変更といった部分は特に苦労することなく習得出来ますし、一応それだけでもサイトの体を保ったものが出来るので、html触りたいけど難しそうって思ってる人はとりあえず簡単な部分から作ってみるとモチベーションの維持になるでしょう。


# 今回覚えたコマンド

```html
<p>hogehoge</p>

```

上の場合は「hogehoge」の部分を出力します。</p>で改行します。

```html
<p style = "color:red">hogehoge</p>

```

「style = "xxxx"」でxxxxの部分にCSSを書けます。この機能で文字色を変化させたり、文字の大きさを変更させたりもできます。

color:色の変更

font-size:文字サイズの変更

background-color:文字の後ろの色の変更

```html
<a href = "x">y<a>

``` 

href = "x"の「x」の部分にサイトURL、「y」の部分に任意の文字を入力すると、サイト上のyをクリックすることで指定したURLに飛べます。

```html
<title>xxxx</title>

```

タブのサイト名を「https://...」から「xxxx」の部分に書いた任意の文字列に変えることができます。

Twitterのリンク貼りはTwitter公式の[https://about.twitter.com/ja/resources/buttons](https://about.twitter.com/ja/resources/buttons)からhtml用のリンクを入手出きるのでそれを利用しました。

このように本当に基礎中の基礎を触っただけです。自分用のメモ書きと初めて触る人の参考になればいいなぁ程度ですが参考にしていただければうれしいです。

また、当サイトの[https://www.calc.mie.jp/posts/2017-04-25-browser-develop.html](https://www.calc.mie.jp/posts/2017-04-25-browser-develop.html)でも言及されていますが、

```html
<head>
  <meta charset="utf-8"/>
</head>

```

と記述しておかないと一部環境で文字化けを起こしてしまうので気をつけましょう。

# 今後の目標

今後はもっとJava Scriptなども使って動きのある機能や、サイトのデザイン面、画像の挿入などをしていきたいです。追加していく機能はべあーずさいとの「コンテンツ」の部分に増やしていく予定です。
