---
title: "freeglutのちょっとだけ"
author: "SKsan_9642_univ"
---

# freeglutで躓いたところ
[GPU並列図形処理入門](http://gihyo.jp/book/2014/978-4-7741-6304-8)という本があったので気になってやってみました．この本では，**OpenGL**を使ったグラフィックスの並列処理を紹介しています．そこでは，OpenGLを扱いやすくするために，**freeglut**を使うのですが，この本が少しだけ古いのと，自分があまりにも無知だったため，解決に時間がかかりました．ここではコードをビルドして実行するまでにぶち当たった壁とその解決方法を紹介します．freeglutのインストールからビルドするまでの説明は[ここ](http://dronevisionml.blogspot.jp/2015/05/openglvisual-studio-2015.html)
を参考にするといいです．~~(最初に見とけばよかった)~~

## 環境
まずはじめに，既に設定済みの環境を紹介しておきます.  
OS : Windows10  
Visual Studio 2013-2017

この本ではVisual Studio 2010を使っていました．


## freeglutのダウンロード
恥ずかしいことにまずここで躓きました．freeglutは
[freeglut](http://freeglut.sourceforge.net/)の[Downloads...](http://freeglut.sourceforge.net/index.php#download)ページの**Stable Releases** からダウンロードできます．
ダウンロードしたファイルを解凍し…たかったのですが，標準で.gzファイルを解凍する機能はWindowsが持っていないため解凍ソフトをインストールし(自分は[7-zip](https://sevenzip.osdn.jp/)を使いました)，解凍します．

この本では**freeglut-2.8.1.tar.gz**(この本が出版された当時の最新版)を解凍すると，フォルダ内に「Visual Studio」というフォルダができると書かれています．  
無知な僕は「VSが最新Ver.だから」という理由で **freeglut-3.0.0** をダウンロードしたわけですが，このファイルを解凍・展開しても「Visual Studio」というフォルダはありませんでした．どうやら，*Ver.3.0.0*で仕様が変わったらしく，おとなしく*Ver.2.8.1*をダウンロードする羽目に…

## インストールと.dllファイルのコピー
**freeglut-2.8.1/Visual Studio**にはVisual Studioのバージョンごとのファイルが有るのですが，2012よりあとのバージョンはなかったのでとりあえず2012内の*freeglut.slnを使いました．ココらへんの詳しい話は[最初に紹介したページ](http://dronevisionml.blogspot.jp/2015/05/openglvisual-studio-2015.html)のやり方でうまくいきました．問題があったとすれば，VSが複数バージ
ョンあるため，生成した.ファイルをどこに入れればいいのか探したことくらいです．(本やサイトごとに入れるものや場所がバラバラなので…)  
結果としてはそれぞれ，  
```
freeglut-2.8.1/include/GL/{freeglut.h,freeglut.h,freeglut_ext.h,freeglut_std.h}->
Program Files (x86)\Windows Kits\10\Include\10.0.15063.0\um\gl
freeglut-2.8.1/lib/x64/freeglut.lib->
C:\Program Files (x86)\Windows Kits\10\Lib\10.0.15063.0\um\x64
freeglut-2.8.1/lib/x64/freeglut.dll->
C:\Windows\System32
```
にコピー．無事OpenGL構築を終えることができました．上記の**10.0.15063**というフォルダはWindows 10のバージョンです．freeglut.slnを読み込む際に2013以降のバージョンだとソリューションのアップグレードというポップアップとともにこの数字列が出てくると思います．基本的にはアップグレードしたバージョンのフォルダに入れれば良いはずです．

## ウイルス対策ソフト対策

無事構築も終わり，`Cntl+F5` でコード生成とともに実行、、、のはずが一向に始まりません．しばらくすると「プログラムを停止しました」というウイルス対策ソフトからの通知が…というのも，VS 2017はまだいれたばかりでなにもプロジェクトを作っていなかったので例外処理を施すのを忘れていたのでした．対策ソフトのアプリから例外するフォルダを選択して適用すればちゃんとプログラムが動いてくれました．

## 最後に

今回自分が躓いたところは，他の人からみたら「当たり前だろ」と思ってしまうかもしれませんが，自分と同じような壁に当たった人の助けになれば幸いです．これから少しずつOpenGLと並列処理について投稿していこうかな，と思います．

### 参考文献
- [GPU 並列図形処理入門――CUDA・OpenGLの導入と活用](http://gihyo.jp/book/2014/978-4-7741-6304-8)(乾正知　著，技術評論社出版)
- [freeglut公式HP](http://freeglut.sourceforge.net/)
- [OpenGLのインストール（Visual Studio 2015 & 2013-DroneとVisionとMachine learning](http://dronevisionml.blogspot.jp/2015/05/openglvisual-studio-2015.html)
- [GLUTによる「手抜き」OpenGL入門](https://tokoik.github.io/opengl/libglut.html)


#### P.S.
Nugetを使ったインストール方法もあったみたいです．こちらのほうがもっと簡単だった…
->[Visual Studio 2015 で OpenGL - Ego.log](http://egolog.hateblo.jp/entry/2016/04/09/212608)
