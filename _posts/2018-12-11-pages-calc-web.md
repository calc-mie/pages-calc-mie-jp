---
layout: post
title: "2018年8月8日式年遷宮期"
author: "flow_6852"
---


計算研究会ではVPSサーバーを借りてホームページの運営、管理を行っています。
サーバーの運用、管理の能力の継承のために半年に一回サーバーの移行を行っています。計算研究会では式年遷宮と呼ばれています。今回はその記録を書いていこうと思います。

内部向け資料です。

今回選んだOSはCentOS7.6.1810です。

下の記事を参考にこのホームページの設定を行いました。

[https://www.calc.mie.jp/posts/2017-07-12-sengu.html](https://www.calc.mie.jp/posts/2017-07-12-sengu.html)

今回は元のサーバーが落ちていたので2のファイルの移動は行いませんでした。
また、公開鍵を登録するシェルスクリプトを書いて起動しました

<publickey.sh>
```
#!/bin/bash

if [ -z $1 ] ; then
    echo "User unspecified."
    exit -1
fi

user=$1
read key
home=/home/${user}
aukeys=/home/${user}/.ssh/authorized_keys

echo "Adding key of $user..."

sudo runuser -l ${user} -c "umask 077; mkdir -p $home/.ssh; echo \"$key\" >> $aukeys"

echo "Kimatta."

```

## 1.calc-webのインストール

[stack](https://www.haskellstack.org/)が必要なのでstackをインストールします。

```shell
 $ curl -sSL https://get.haskellstack.org/ | sh
 $ stack setup
 $ stack path
 $ stack exec env
```

calc-webをダウンロードします。

```shell
 $ git clone https://github.com/calc-mie/calc-web/
```

calc-webのビルドをします。

```shell
 $ cd calc-web
 $ make install
```

もしくは

```shell
 $ cd calc-web
 $ stack build
 $ stack exec calc-web build
```

`make install`もしくは`stack build`中にエラーが起こった場合はパッケージが足りないと思われるので`yum install`してください。(haskellやstackの知識が無いですが勉強中なのでcalc-webの動作を追えるようになったら解析して足りなかったり間違った情報は更新及び追記をしていきます。今回は`gmp-devel`が足りなかった？)

## 2.pagesの整備

計算研究会のメンバーが各自でホームページを作りたい時に利用してもらう
[https://pages.calc.mie.jp](https://pages.calc.mie.jp)
の整備を行いました。
