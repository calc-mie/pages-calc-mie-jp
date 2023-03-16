---
title: "ホームページ作ってみた　その２"
author: "Bear_0821"
---

サイト作りの続きです。

# 概要

サイトURL：[https://pages.calc.mie.jp/bear0821/](https://pages.calc.mie.jp/bear0821/)


今回は電卓を作りました。

htmlの中にjava Scriptを書き込む形で使用しました。ファイルからの呼び出しも覚えなければ…。

# 今回覚えたコマンド

```html
<button>xxx</button>

```

ボタンを作る関数です。上の例の場合は「xxx」というボタンが作成されます。
しかし、これだけではボタンが作られるだけでクリックしても何も起きません。そこで、

```html
<button onclick="alert('false');">警告</button>

```

「onclick」を用いることでボタンを押された時の機能を実装できます。
例としてJava Scriptの「alert」では文字通りアラートを表示することができます。
上の場合は「警告」というボタンを押すと「false」というアラートが表示されます。

「onclick」の=の後にはJava Scriptを書くことができます（alertもJava Scriptです）。
Java Scriptを勉強することでできることは増えていきます。


これ以外にも演算や文字の表示なども行うことができるので、サイトを作成するにあたってJava Scriptの習得はとても重要でしょう。htmlの学習と並行して勉強していきたいです。



次回以降はJava Scriptをより理解するために以前から興味のあったゲーム作りをやっていきたいと思います。
きっと最初は躓きまくると思いますが間違えて覚えるほうが性に合っているので頑張ります。

電卓は[https://pages.calc.mie.jp/bear0821/calculator.html](こちら)

