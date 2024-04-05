---
layout: post
title: "Surface Pro 3にlinuxを導入した"
author: "flow_6852"
---

僕はlinux環境に興味を持っています.
論文を読んだりノートを取ったりするために最初はiPadを購入しようと考えていましたが,
僕は持っているほとんどの端末がlinuxとなっているためiPadを購入するよりも
何かしらのタブレットを購入してそこにlinux環境を入れる方がメンテナンスがしやすく,
iPadよりも使いこなせるのではと思ってSurfaceにlinuxを入れてiPadのように使うことを目的としました(そしてそれをiPadと呼ぶことにしています).
この記事は今後同じようなことをするかもしれないので備忘録として残しておきます.

# ハードウェアの購入

僕はSurface Pro 3(本体とタイプ入力カバー)のバルク品が安かったためそれを購入し,
充電器やペンがなかったためサードパーティ製のものを,フィルム合わせて一つずつ追加で購入しました.
それぞれ順に.15290円,3580円,5990円,945円です.

# linuxのインストール

ArchLinuxを導入しました.([archwiki install guide](https://wiki.archlinux.jp/index.php/%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%82%AC%E3%82%A4%E3%83%89))

インストール自体はデスクトップ等と変わりなかったのでそこまで苦労しませんでした.

### 補足

僕の購入したSurface Pro 3は最初からbit lockerとSecure bootがオフになっていたのでそこで苦労はしませんでしたが
もし新品を購入した場合はその2つをオフにしないとインストールに失敗する(起動ができないのほうが正しいかもしれない)ので
bit lockerとSecure bootをオフにするようにしてください.

# その他のアプリケーション(ディスプレイマネージャ等)

主に導入したものは以下の通りです.

([タブレットPC](https://wiki.archlinux.jp/index.php/%E3%82%BF%E3%83%96%E3%83%AC%E3%83%83%E3%83%88_PC)と
[archwiki Surface Pro 3](https://wiki.archlinux.jp/index.php/Microsoft_Surface_Pro_3)を参考にしました)

+ [yay](https://aur.archlinux.org/packages/yay/)
+ [lightdm](https://wiki.archlinux.jp/index.php/LightDM)
+ [light-locker](https://wiki.archlinux.jp/index.php/%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E4%B8%80%E8%A6%A7/%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3#.E3.82.B9.E3.82.AF.E3.83.AA.E3.83.BC.E3.83.B3.E3.83.AD.E3.83.83.E3.82.AF)
+ [i3-mw](https://wiki.archlinux.jp/index.php/I3)
+ [alacritty](https://wiki.archlinux.jp/index.php/Alacritty)
+ [fcitx](https://wiki.archlinux.jp/index.php/Fcitx)
+ onboard
+ xournalpp(AUR)
+ easystroke
+ [iio-sensor-proxy](https://gitlab.freedesktop.org/hadess/iio-sensor-proxy/)

# モニタの自動回転について

[Linuxで画面＆タッチスクリーンを90度回転](http://bluearth.cocolog-nifty.com/blog/2019/12/post-e5f4f1.html)を参考に自作のbashスクリプトを作成しました.

``` bash
#!/bin/bash

while read i ; do
	check=$(echo $i | grep A | awk -F ':' '{print $2}')
	case "$check" in 
		" normal" ) num=0; rot="1 0 0 0 1 0 0 0 1";;
		" right-up" ) num=3; rot="0 1 0 -1 0 1 0 0 1";;
		" left-up" ) num=1; rot="0 -1 1 1 0 0 0 0 1";;
		" bottom-up" ) num=2; rot="-1 0 1 0 -1 1 0 0 1";;
		* ) continue;;
	esac
	xrandr -o $num
	# xsetwacom set stylus Rotate $rot
	while read i; do
		id=${i#*id=}
		xinput set-prop ${id%%[*} 'Coordinate Transformation Matrix' $rot
	done < <(xinput list | grep pointer | grep NTRG)	
done
```

i3の設定ファイルに`exec --no-startup-id monitor-sensor | ${PATH}/rotate.sh`を追加してあげれば,
モニタを傾けた時に自動でディスプレイとタッチスクリーンを変更してくれます.

# wi-fi接続に関して

ここまでの設定では特に苦しんだところはありませんでしたが,
wi-fiに接続している時に突然繋がらなくなるという問題が発生していました.
これはカーネルモジュール(mwifiex_pcie)が省電力モードをデフォルトで行っていることがわかりました. 
([https://wiki.archlinux.org/index.php/Talk:Microsoft_Surface_Pro_3](https://wiki.archlinux.org/index.php/Talk:Microsoft_Surface_Pro_3))
(もしかしたらまた突然切れるかもしれない)
