---
title: "ブラウザで動作するものを作る"
author: "naca_cyan13"
---

[](
内部向けドキュメント\
ブラウザで動くものを開発するには？\
どんな構造になってるのか？\
htmlとは\
cssとは\
javascriptとは
)

内部向け資料です。

ブラウザは入力されたURLにしたがってサイトにアクセスします。
ブラウザはそのサイトに配置された資源を使い、アプリケーションとして動作させます。
中心的な要素としてHtml、Css、Javascriptがあります。
今回はHtmlがどんなものなのか知るためのチュートリアルをします。

javascriptについては<a href="https://www.calc.mie.jp/posts/2017-04-25-hwtlearnjs.html">こちら</a> 。

# 動作構造

まずアクセスしたURLのHtmlを読み込みます。
そのHTMLを元にサイトを表示するのですが、その際 `<link rel="stylesheet" href="default.css"/>` のような要素が存在していた場合、その資源にアクセスしサイトに反映します。
このようにHtmlから外部の資源を要求し反映することができます
javascriptもHtmlから`<script src="main.js" />"` のように実行することができます。

# チュートリアル(html)

## First Step

簡単なHtmlを作成してブラウザで開いてみます。

```shell
$ pwd
/home/naca_cyan13/html_study/
$ touch index.html
$ emacs index.html
```

`index.html`を以下のように編集。

```html
<html>
    <body>
      hello, html!  
    </body>
</html>
```
ではこの`index.html`をブラウザで開いてみましょう。普段使いのブラウザーのアドレスバーに`file:///home/naca_cyan13/html_study/index.html` と打ち込んでアクセスしてみると、hello, html!と画面に表示されるはずです。

_(注意)`/home/naca_cyan13/html_study/`は私の環境でのパスなので自分の環境のパスに置き換えてください。_

## Second Step

日本語も表示してみたいですね。日本語も表示したい時、ブラウザに文字コードをわたしてあげないと行けません。`index.html`を以下のように編集してブラウザで開いてみましょう。

```html
<html>
    <head>
      <meta charset="utf-8"/>
    </head>
    <body>
      <p>hello, html!</p>
      <p>わたしはnaca_cyan13です!</p>
    </body>
</html>
```

`<meta charset="utf-8"/>` はブラウザにこのhtmlはこの文字コードを使用していますよと指定するためのものです。日本語を表示したい時は忘れずにつけておきましょう。

`<p>`タグはParagraphの略で、`<p>～</p>`で囲まれた部分がひとつの段落であることを表します。
試しに`<p>`タグを消したりつけたりして実験してみましょう。

## Third Step

おまけです。Htmlには表や列挙表現、図の挿入などがあるのでサンプルを貼っておきます。

### 表`<table></table>`

```html
<table>
    <thead>
        <tr>
            <td>列1</td>
            <td>列2</td>
            <td>列3</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>11</td>
            <td>12</td>
            <td>13</td>
        </tr>
    </tbody>
</table>
```

### 列挙`<ul><li></li></ul>`

```html
<ul>
    <li>サーバル</li>
    <li>アライグマ</li>
    <li>フェネック</li>
</ul>
```
### 図`<img/>`

```html
<img border="0" src="../images/ta-nosi-.png" width="128" height="128" alt="わーい">
```

javascriptについては<a href="https://www.calc.mie.jp/posts/2017-04-25-hwtlearnjs.html">こちら</a> 。


