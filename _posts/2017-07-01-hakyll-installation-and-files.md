---
layout: post
title: "Hakyllの使い方 インストールと各種ファイル説明"
author: "mkdagjp"
---

Hakyllのインストール方法と各種ファイル説明
インストール，新規作成の部分はhttps://jaspervdj.be/hakyll/tutorials/01-installation.htmlを参考

# インストール方法
stackが入っているものとします．
インストールは，
```
$ stack install hakyll
```
するだけ．
ただし，メモリが少なめのマシンの場合は，コア数分同時にビルドするとメモリが枯渇するので
```
$ stack install hakyll -j1
```
などとして同時に走らせるビルド数を1つとかに制限したほうがいい．

# 新規作成

```
$ hakyll-init [名前]
```
