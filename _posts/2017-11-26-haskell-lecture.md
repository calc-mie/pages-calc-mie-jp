---
title: "Haskell 講習会を開催しました"
author: "_cyan13"
---

あらたなパラダイムの言語を学びたかったので、Haskell講習会を `naca_nyan` に開いてもらいました。

# やったこと

- Hello, world!
- Hello, <あなたの名前>!
- 関数定義

をやりました。

他にも

- リスト遊んだ
- 代数的データ構造
- 型クラス
- IOモナドを展開しよう！

などやりましたが、これらについては他の人が書いてくれるでしょう。

# Hello,World! と Hello, <あなたの名前>!

Haskellでも他言語のmain関数みたいなものがあるので、そこに処理を書いて行きます。
以下が Hello,World! のコード。

```haskell
main = putStrLn "Hello, World!"
```

実は、この `main` は関数ではなく、アクションの結果が束縛された変数だそうです。（副作用を含んでるからかな？）

次に Hello, <あなたの名前>! のコード。

```haskell
main = do
  name <- getLine
  print $ "Hello," ++ name

```

`do`、`<-`、`$` is 何といった感じではないでしょうか。順番に説明します。

## `$` とは

関数適応演算子です。Haskellでは、空白も関数適応演算子として扱えますが、これは右結合かつ優先度が最強のため、カッコで優先度を指定してやる必要があったり、式が煩雑になるケースが多いです。そういう場合に `$` を使うとスマートに関数適応の優先度を操作できます。たとえば次のコードは上下同値です。

```haskell
print ("Hello," ++ name)

print $ "Hello," ++ name
```

## `do` とは

モナドの文脈を手続き型言語のような書き方で書けるようにするものらしいです。
上下のコードは同値です。


```haskell
main = do
  name <- getLine
  age <- getLine
  print $ name ++ " is " ++ age ++ "years old."

main =  getLine >>= 
  (\name -> getLine >>= 
    (\age -> print $ name ++ " is " ++ age ++ " years old."))

```

下の方、ラムダ式という記法を使っているのですが、ぐちゃぐちゃしてなにがなんだか。`>>=`
とかなんだこれ...って感じですよね。

上の方はフィーリングでなんとなくこうやってるんだなーというのわかりますよね。

## `<-` とは

モナドから値を取り出すものらしいです。

```haskell
main = do
  name <- getLine
  let age = "5"
  print $ name ++ " is " ++ age ++ "years old."

```

このコードの `getLine` というアクション(関数ではないらしい)は

``` 
getLine :: IO String 
```

という型を持っているので、評価して帰ってきた値は `IO String` 型ということから、普通の文字列として扱えません。これから `IO` を外して `String` にし、変数に束縛してくれるものが、`<-` らしいです。

比較として、 `=` は `"5"` が `String` 型なので、 `let` で束縛する事ができますね。

# 関数定義

Haskellの関数定義は、以下のように行います。

```haskell
addone :: Int -> Int
addone x = x + 1 
```

一行目のやつは、型注釈と言います。今回の場合だと、 `+` が使われているので、数が扱われるというのが推論できるので、入りませんが、型注釈をつけないとコンパイルが通らない場合があるそうです。

## 強力なパターンマッチ！！！！

Haskellには超強力なパターンマッチという機能があります。

```haskell
operate :: Char -> Int -> Int -> Int 
operate '+' = (+)
operate '-' = (-)
operate '*' = (*)
operate '/' = div
operate _   = const

main = do
  sa <- getLine
  sb <- getLine 
  so <- getLine 
  let a = read sa
  let b = read sb
  let co = head so
  let o = operate co
  print (o a b)
```

`operate` 関数は「文字一つ受け取って、対応する2項演算子を返す関数」です。
見てわかるように、引数がこうだったらこう という処理を if文などを使うことなく表現できています。

# 参考文献

大川徳之 『関数プログラミング実践入門』 技術評論社
