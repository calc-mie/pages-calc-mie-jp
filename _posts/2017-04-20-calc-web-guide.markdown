---
title: "calc-webの投稿ガイド"
author: "naca_cyan13"
---

計算研究会では活動の一つとして数学、物理、情報工学に関する知識を記事にするという物があります。
その記事はcalc-webといってcalc-argon(2017/4/20現在)サーバーで動いています。

# 投稿方法

まずはcalc-argonに接続(ssh)

```
$ ssh j4158**@calc.mie.jp
```

記事を管理するディレクトリに移動します。

```
$ cd /home/share/calc-web
```

記事作成用のシェルスクリプト`new-post.sh`を起爆して、title、authorを設定します。

```
$ ./new-post.sh
title?> sample
author?> naca_cyan13
Creating posts-available/2017-04-20-sample.md...
Done.
```

記事を編集します。

```
$ emacs posts-available/2017-04-20-sample.md
```

```
$ cat posts-available/2017-04-20-sample.md
---
title: "sample"
author: "naca_cyan13"
---

This is sample post!(この辺を編集する)
```

編集したらシンボリックリンク操作をしたあとビルドをします。

```
$ cd posts
$ ln -s ../posts-available/2017-04-20-sample.md ./
$ cd /home/share/calc-web/
$ make
```


# 命名のルール

`new-post.sh`で記事のタイトルを設定するときは極力

- 小文字英語。
- 単語は`-`で区切る。

のようにしましょう。

例)
calc-web-guide
typescript
slack-notification




