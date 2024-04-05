---
title: "Visual Studioでの実行ファイル設定"
author: "feeling_grasper"
---

### 実行ファイルのアイコン設定

Win32コンソールアプリケーションプロジェクト(C++)で実行ファイルを生成すると、デフォルトアイコンを使ったものが生成される。これを変更したいと思った。
まず、アイコン画像としたいico形式のファイル(hoge.icoとする)を用意する。
次にhoge.rcのようにリソースファイルを作成し、

　```HUGA ICON "hoge.ico"```

のように記述する。ファイル名は任意。`HUGA`の部分も任意。
`DISCARDABLE`とか`FIXED`とか追加で書いたりすることもあったみたいだけど、16-bit Windowsのものみたい。詳細はこちら → [ Common Resource Attributes](https://msdn.microsoft.com/en-us/library/aa380908(VS.85).aspx)
ソリューションエクスプローラーのResource Files内にそれらを配置してビルドすると、アイコンがついた実行ファイルが生成される。


### 実行ファイルのタイトル名設定
上と同じ状況で、生成した実行ファイルを起動した際、タイトルバーにはデフォルトで実行ファイルの場所が表示される。それを変更しようと試みた。

```
	SetConsoleTitle(TEXT("Hoge"));
```

対処としては、このコードをmain関数に埋め込むだけでよかった。ここでは`Hoge`がタイトル名に相当する。詳細はこちら→[SetConsoleTitle function](https://msdn.microsoft.com/ja-jp/library/ms686050.aspx)

### 感想
もっとガリガリ書くものだと思ったけど、そうでもなかった。あと、この記事に載せたリンク先が二つとも英語で、英語読めないとやっぱりやっていけなさそうだなぁと思った。

