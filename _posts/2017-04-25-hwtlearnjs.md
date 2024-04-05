---
layout: post
title: "javascriptの勉強"
author: "naca_cyan13"
---

[](
javascriptとは\
tutorial\
main.jsを編集する。\
index.htmlが読み込まれた時にmain.jsを実行するようにする。\
jQueryでhtmlをjavascriptから変更する。
)

Javascriptはブラウザ上で実行することができるスクリプト言語です。C言語と違い動的型付けであったり、コンパイルをせずそのままほり込むことで実行することができます。

# 実行方法

`main.js`というファイルを作成し、以下のように編集します。

```javascript
document.body.innerHTML = "hello, javascript!";
```

次に`index.html`を作成し、以下のように編集します。

```html
<html>
    <head>
        <meta charset="utf-8"/>
    </head>
    <body>
    </body>
    <script src="main.js"></script>
</html>
```

この時ディレクトリ構造は以下のようにしてください。

```
./ - + - index.html
     + - main.js
```

_`./`は現在のディレクトリ_

では`index.html`にアクセスしてみましょう。hello, javascript!と表示されるはずです。

動作の流れは

- ブラウザが`index.html`にアクセスする。
- `<script src="main.js"></script>`を読み込み実行する。
- `document.body.innerHTML = "hello, javascript!"`が実行される。
- bodyの内容が書き換わる。

といった感じ。

# 重要なライブラリ(jQuery)

上記では`document.body.innerHTML`というものに文字列を代入してbodyの内容を書き換えました。
ここではHtmlの書き換えをjavascriptで簡単に行うためのjQueryの短い紹介をします。


jQueryとはセレクタというものを使い、Htmlにあるドキュメントを指定し、その内容をかきかえたりするのがおもな機能のjavascriptのライブラリです。
以下はボタンがおされたらすべての`<p>`タグの内容をButton is clicked!にするというものです。

```html
<html>
    <head>
       <meta charset="utf-8"/> 
    </head>
    <body>
        <script src="https://code.jquery.com/jquery-1.11.1.min.js"></script>
        <p>サーバルはですね、基本的にはアフリカのサバンナと言われる地域で過ごしてまして、</p>
        <p>若干草が生えてるところなので、そういったところで歩きやすいようにサーバルは細長い個体で。</p>
        <p>あと耳も大きいので、遠くの音を聞こえるように。ジャンプ力ですかね……。高いところにスッとジャンプできる動物でして。</p>
        <p>高いところが好きなので、軽々と、1m2m余裕でジャンプしてくれます。</p>
        <button onclick="$('p').text('Button is clicked!')">ボタン</button>
    </body>
</html>
```

実行結果が<a href="https://pages.calc.mie.jp/sUgarCubeBox/jquery.html">こちら</a>。

# 学習の深め方

TODOリスト、数値計算機、簡単なクイズゲームなど一度作ってみると大きなスキル向上になります。また、javascriptを使う上ですでにあるライブラリを使用出来るようになるとやれることがかなり増えます。上記で紹介したjQueryの他に、ドキュメントを操作する系のものとしてreact.jsやriot.jsがあります。ゲーム関連ではenchant.jsやpixi.js、phaser.ioなどがあげられます。一つのライブラリの学習を深めるのではなく、目的に対してライブラリを選択し、使い方を理解するという力を鍛えると良いでしょう。





