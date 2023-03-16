---
title: "Growiを計算研究会のwikiとして利用を開始しました"
author: "flow_6852"
---

# はじめに

計算研究会では以下の2つのツールを用いていました.

1. 学祭の会議の議事録や$n$人で集まってゼミをする$n$頭勉強会の共有資料として HackMD(https://hackmd.io)
1. https://wiki.calc.mie.jp のサーバアプリケーションとしてdokuwiki(https://www.dokuwiki.org/)

HackMDを使って複数人で文書を操作し,
出来上がったものをwikiに保存,継承するという形式をとっていました.

しかし,別々のmarkdownの方言を使っているのでwikiへの保存がかなり大きなタスクとなっていました.
この点を解決する方法を探していたところ,Growi(https://github.com/weseek/growi-docker-compose)がモダンで使いやすいGUIを持っていて良さそうだったので導入してみたところかなり好評でした.

この記事ではGrowiのセットアップで特に困った点を記述します.

# 手順

1. docker-composeをインストールする(https://docs.docker.jp/compose/install.html)
1. growi-docker-composeをクローンして各種設定をする.
1. docker-compose up -dでサーバを立ち上げる
1. systemdのファイルを作成する.

# 各種設定(抜粋)

今回はCodiMD(md.calc.mie.jp)とGrowi(wiki.calc.mie.jp)を
それぞれ別のドメインに割り当てました.
Growiのconfigで設定すべき環境変数を以下に示します.

+ docker-compose.yml

```
services:
 app:
  ports:
   - 3000:3000
  environment:
   - HACKMD_URI=https://md.calc.mie.jp 
   - APP_SITE_URL=https://wiki.calc.mie.jp
```

+ docker-compose.override.yml

```
services:
 hackmd:
  environment:
   - GROWI_URI=https://wiki.calc.mie.jp
   - CMD_PORT=3100
   - CMD_ALLOW_ANONYMOUS=false
  port:
   -3100:3100
```

+ nginxのmd.calc.mie.jpのためのconfig

```
server {
        server_name md.calc.mie.jp;
}

server {
        # CodiMD
        location / {
                proxy_pass http://127.0.0.1:3100;
        }
}
```

+ nginxのwiki.calc.mie.jpのためのconfig

```
server {
        server_name wiki.calc.mie.jp;
}

server { 
        # Growi
        location / {
                proxy_pass http://127.0.0.1:3000;
        }
}

```

## 現在起こっているエラーと暫定的な回避方法

`CMD_ALLOW_ANONYMOUS=false`の状態で作られたGrowiのページは永久的に(?)HackMD連携が行われませんでした(解決しませんでした...)
GrowiクライアントからCodiMDのページに複製するときにANONIMOUSで新規ページを立てることになるからかと考えていますが,
`CMD_ALLOW_ANONYMOUS=false`でない状態で作成されたページを`CMD_ALLOW_ANONYMOUS=false`の状態で起動した状態でHackMD連携をすると正常な動作をするのでよくわかっていません.

暫定的な回避方法として,CodiMDにアカウントを登録してGrowiクライアント内でログインして新規ページの作成をするとうまく連携がとれるようです.

# まとめ

https://calc.mie.jp は外部向けの文書を公開し,
https://wiki.calc.mie.jp は内部向けの文書を公開しながらも蓄えておくように運用していきます.
