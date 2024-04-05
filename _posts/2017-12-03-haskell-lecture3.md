---
title: "Haskell 講習会を開催しました(3)"
author: "@naca_nyan"
---

Haskell講習会でちょっとだけ触れた型クラスとIOモナドについて書きます。

# 型クラス
Haskellは多相型(polymorphic type)をサポートしていますが、型クラスを使うと多相性を制御することができます。
Haskellの文脈では、フルに多相性を使う方を単に polymorphism といい[^1]、型クラスの方はAd-hoc polymorphismといったりします。

[^1]: 明示的にこっちを指したいときは parametric polymorphismと言います。

Int型の値を取り出せそうな型という型クラスを作ります。
```haskell
class Integerable a where
  toInt : a -> Int
```
`Int`はそのものがIntなのでIntegerableです。
```haskell
instance Integerable Int where
  toInt = id
```
`Bool`も`True`が1で`False`が0と捉えることで自然にIntにできます。
```haskell
instance Integerable Bool where
  toInt True  = 1
  toInt False = 0
```
`Maybe a`も同じようにIntっぽくできます。
```haskell
instance Integerable (Maybe a) where
  toInt (Just _) = 1
  toInt Nothing  = 0
```

Integerableな値を、Intにして足し算する関数を書いてみます。
```haskell
add :: (Integerable a, Integerable b) => a -> b -> Int
add x y = (toInt x) + (toInt y)
```
`(Integerable a, Integerable b) =>` という部分を **型制約** といい、型変数 `a`, `b` が`Integerable` のインスタンスであることを要請しています。 これによって `a` 型の `x` や `b` 型の `y` に対して関数 `toInt` が使えることが保証されます。

# IOモナドを分解する
[IOモナドを素手で触ってみた](https://qiita.com/7shi/items/0a90d7ba31355e1c73aa) という記事を見ながらIOモナドを分解して遊びました。

Haskellには `RealWorld` という型があり、理論的にはこれに実世界すべてのものが入っていることになっています。ここではそれだと考えにくいので、 `RealWorld` はstdout(標準出力)だと思います[^2]。

[^2]: 実際には他にも標準入力や日時の情報、ファイルなども入っています。

IOの実態は次のようなものです(これは実際のHaskellコードではなく理解のための不正確なものです)。
```
type IO a = RealWold -> (RealWorld, a)
```
例えば、 `IO Int` 型ならば、その実態は `RealWorld -> (RealWorld, Int)` なので、 `RealWorld` 型の値を受け取って、別の `RealWorld` 型の値と `Int` を返す関数のことなのです。
もう少し具体的に、 `putStr "hoge" :: IO ()`  という関数を考えると、これは `RealWorld` 型の値を受取り、その中の標準出力に文字列 `hoge` を追加した `RealWorld` と、意味のない値 `()` を返します。`IO ()` は実質 `RealWorld -> RealWorld` なので、現実世界の変更にしか興味がないということです。

実際にGHCi上で上に述べたような関数を取り出してみます。
```
$ ghci
> :set -XUnboxedTuples
> import GHC.Base
> let f = unIO $ putStr "hoge"
> :type f
f :: State# RealWorld -> (# State# RealWorld, () #)
```

なんかよくわからない#がいっぱいありますが、実質 `RealWorld -> RealWorld` な関数 `f` が取り出せました。やった〜
