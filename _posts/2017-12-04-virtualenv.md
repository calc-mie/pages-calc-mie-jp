---
title: "Virtualenv は便利だよ"
author: "_cyan13"
---

pythonでなにかを開発する上で、いろいろパッケージを使う必要がでてきます。その時、あるパッケージをアップデートしないとそれに依存する別のパッケージが動かないという場合があります。しかし、アップデートすると他の開発環境と競合したりと面倒ごとがいろいろ起こってしまいます。

それを解決するのが **virtualenv** です。

# virtualenv  とは

virtualenvは仮想的な開発環境をいろいろ分けて使うことを可能にするものです。例えば、Aという環境にはpython3.1が入っているが、Bという環境にはpython2.7が入っているという状況を作ることができます。

# インストール

```bash
# pip install virtualenv
```

# 使い方

新しい環境を作るってそこにいくつかパッケージを追加してみましょう。

## 新しい環境の作成、環境に入る

まず環境を作るコマンドが以下。

```bash
$ virtualenv testenv
```

ここで`testenv`は環境の名前です。このコマンドを叩くと、現在のディレクトリに`testenv/`というディレクトリができます。そのディレクトリの中を調べてみると、

```bash
$ cd testenv
$ ls
bin  include  lib  local  pip-selfcheck.json
```

いくつかディレクトリやファイルがあります。これら**testenv**環境の情報を保存するものです。この中の`bin`に入って、`activate`という環境の中に入るスクリプトを起動してみましょう。

```bash
$ cd bin
$ source activate
(testenv) $ 
```

ここで注意すべきなのが、`source`でスクリプトを起爆しなければ、環境には入れないということです。

`(testenv)` という表示がプロンプトの頭についていれば、あなたは**testenv**環境に入ることができています。

## 環境にパッケージを入れる

それではこの環境にいくつかパッケージを入れてみましょう。

```bash
(testenv) $ pip install numpy tensorflow keras
```

ここで、pipコマンドの実行権限が`$`になっていることに注目してください。testenv環境のパッケージは、全てtestenvディレクトリの中にあり、そのディレクトリの権限は環境の作成者のものになるので、パッケージをインストールするのも、ルート権限を使わなくともよいのです。

## 環境から出る

virtualenvの中に入ると、`deactivate`というコマンドが使えるようになっています。このコマンドを起爆するとその環境からでることができます。

```bash
(testenv) $ deactivate
$
```

# まとめ

最後に、virtualenvの基本操作の機能をまとめます。

|コマンド|役割|
|:---|:---|
|`$ virtualenv <環境名>`|新しい環境を作る。|
|`$ source <環境名>/bin/activate`|環境に入る。|
|`$ deactivate`|その環境から出る。|

### 参考文献

- Virtualenv - https://virtualenv.pypa.io/en/stable/


