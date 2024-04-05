---
layout: post
title: "競技プログラミング用にPythonの環境を整える"
author: "D4prog"
---

### このドキュメントの目的
電算演習室からICPC国内予選に参加する場合を想定した、必要最小限快適なPythonのコーディング環境を整える手順を示す

* [Python ドキュメントのダウンロード](#Python%E3%83%89%E3%82%AD%E3%83%A5%E3%83%A1%E3%83%B3%E3%83%88%E3%81%AE%E3%83%80%E3%82%A6%E3%83%B3%E3%83%AD%E3%83%BC%E3%83%89)
* [Jupyterの使用](#Jupyter%E3%81%AE%E4%BD%BF%E7%94%A8)
<hr />
* [Python実行環境の用意](#Python%E5%AE%9F%E8%A1%8C%E7%92%B0%E5%A2%83%E3%81%AE%E7%94%A8%E6%84%8F)

#### 結論だけ先に示す
```shell
$ git clone --depth 1 https://github.com/python-doc-ja/py35.git python-3.5-docs-ja-html
$ jupyter notebook
```

#### 実行環境の用意について
最終節の手順の実行は**電算演習室において必要ではない**。
電算演習室では Python 3.5.2 と Jupyter がインストールされているので、[Python 実行環境の用意](#Python%E5%AE%9F%E8%A1%8C%E7%92%B0%E5%A2%83%E3%81%AE%E7%94%A8%E6%84%8F)はドキュメントの最終節に示した。
ICPC国内予選で Python 3.6.1 が使用可能なシステムが用意されるとは思えないので、電算演習室の素のPythonをJupyterから用いる前提で話を進める。

### Pythonドキュメントのダウンロード
[Welcome to Python.org](https://www.python.org) >  
[Documentation](https://www.python.org/doc/) >  
[Documentation Releases by Version](https://www.python.org/doc/versions/) >  
目的のバージョンのドキュメントページ >  
Download these documents  
例えば、3.5.2 [Download Python 3.5.3 Documentation](https://docs.python.org/3.5/download.html) からドキュメントをダウンロードします。

bz2なので、`tar zxf` ではなく `tar jxf` あるいは単に `tar xf` を使って解凍します
```
$ tar xf python-3.5.3-docs-html.tar.bz2
```


ですが、日本語のドキュメントを入手したい場合、
```
$ git clone --depth 1 https://github.com/python-doc-ja/py35.git python-3.5-docs-ja-html
```
というふうにして日本語訳をダウンロードするのが楽かと思われます



### Jupyterの使用

Jupyterはいいぞ

**あとで書く**

```
/path/to/icpc-coding-dir/ $ jupyter notebook
```

### Python実行環境の用意
(電算演習室では Python 3.5.2 と Jupyter がインストールされているのでこの節は必要ありません)

#### 依存ライブラリのインストール
##### openssl-dev
電算演習室では `openssl-dev` がないので、sslモジュールが効かなくなって、環境を作ったあとpipでモジュール落としてこれない(httpsで繋ぎに行くので)事になります。
それは困るので

[OpenSSLのソースコード](https://www.openssl.org/source/)を入手して、インストール

```
$ ./config -fPIC shared --prefix=$HOME/path/to/openssl/
$ make
$ make test
$ make install
```
`LD_LIBRARY_PATH` にライブラリパスを追記

##### sqlite-devel
`sqlite-devel` がないとJupyterが起動しないので、インストール

まだインストールしてない**あとで書く**

#### Pythonのインストール
```
env CFLAGS=-I$HOME/path/to/openssl/include LD_LIBRARY_PATH=$HOME/path/to/openssl/lib make
```

#### venvモジュールの使用法

**あとで書く**


```python

```
