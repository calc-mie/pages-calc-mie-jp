---
title: "calc-tweetの使い方"
author: "flow_6852"
---


計算研究会の連絡は主にslackとtwitterで行われています.これらの連携やcalc-webの投稿を二つのSNSに連絡,告知するアプリを作成しました.使用言語はHaskellです.

[ソースコード](https://github.com/calc-mie/calc-tweet)

twitterのcalc_mieというアカウントにDMで以下のコマンドを送ります.ただし権限が必要です(権限の付与については後述).

#### 連絡内容をセットする
##### 入力形式
```
 $notice 「連絡したい内容」
```
`[連絡]「連絡したい内容」`という文字列がメッセージの先頭に配置されます.

#### 日付,時間,場所をセットする
##### 入力形式
```
 $date [-(数字)] 「日付」
 $time [-(数字)] 「時間」
 $locale [-(数字)] 「場所」
```
第一引数の数字の一致するもので`「日付」 「時間」＠.「場所」`という文字列が配置されます.
入力されない場合は空白になり,場所の後に空白が入ります. [-(数字)]がない場合は1とされます.
入力が重複された場合は最新のデータを採用します(入力例を参照してください).

また,日付と時間がセットされた場合,一番早く始まる時間にtwitter側で一時間前にリツイートされます.

#### 連絡内容をPOSTする
##### 入力形式
```
 $post
```
セットした文字列をtwitterとslackにpostします.`$notice`をしていないとpostされません.

#### 今までの入力をリセットする
##### 入力形式
```
 $clear
```
セットした文字列を一からの状態に戻します.



#### calc-webの更新の通知をPOSTする 
##### 入力形式
```
 $post-calc-web 
```
calc-webを投稿して完成したらこれを送ってください(もしくは権限を持っている人にお願いしてください).

#### 利用権限を渡す
##### 入力形式
```
 $useradd 「アカウント(twitterのid)」
```
引数にしたアカウントに使用権限を与えます.

#### プレビューをDMに出力する
##### 入力形式
```
 $print
```
`$post`したときにどのような出力になるかをDMで確認できます.

## 入力例

```
$notice post test
$date 5/15(水)
$notice これはテストです.
$time 10:30~11:30
$locale 電算
$time -2 10:40
$locale -3 電算
$date -2 5/16(木)
$date 5/16(木)
$post
```

## 出力例
```
[連絡]
これはテストです.
5/15(木) 10:30~11:30 ＠.電算
5/16(木) 10:40
 ＠.電算
```

## つくってみて
つらかった.
先人の知恵をたくさん借りて作成したので与えられる側になれたらいいなぁと思います.

### 参考文献
 * [https://techracho.bpsinc.jp/jhonda/2017_12_18/49797](https://techracho.bpsinc.jp/jhonda/2017_12_18/49797)
 * [https://qiita.com/kentahama/items/261c9c86d02161680933](https://qiita.com/kentahama/items/261c9c86d02161680933)