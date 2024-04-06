---
layout: post
title: "Haskell 講習会を開催しました(続き)"
author: "SKsan"
---

[前回の記事](https://www.calc.mie.jp/posts/2017-11-26-haskell-lecture.html)の続きをまとめたいと思います．
この記事では

- リスト構造
- 代数的データ構造

について講習会で学習したことを紹介しします．

# リスト構造をあつかう
Haskellでは，リスト構造を簡単に扱うことができます．
```haskell
> let xs = [1,2,3]
> xs
[1,2,3]
> head xs
1
> tail xs
[2,3]
```
これはHaskellを対話的に評価できるghciを用いた実行結果です．1行目でリストの生成，headはリストの先頭の要素を返す関数，tailはリストの先頭要素以外のリストを返す関数です．ここで変数名(?)が`xs`となっているのは`(変数)x'(複数形)s`という意味だそうで，Haskellで複数の要素を表すときに用いられる慣習のようなものらしいです．

## 要素の追加
リストに要素を追加します．要素を追加するには`:`か`++`を使うことができます．
```haskell
> 2 : xs
[2,1,2,3]
> [4] ++ xs
[4,1,2,3]
```
ここで追加する要素に注目してみると，`[]`で囲まれていない`2`と，囲まれている`[4]`が出てきます．これは`2`が値であり，`[4]`がリストであることを意味します．`++`，`:`のそれぞれの型は，
```haskell
> :type (:)
(:) :: a -> [a] -> [a] 
> :type (++)
(++) :: [a] -> [a] -> [a]　
```
です．この型に合わない式，例えば
```haskell
> [3] : xs
```
や
```haskell
> 5 ++ xs
```
などの書き方はエラーとなります．`++`や`:`は他の関数のように記述することができ，
```haskell
(:) 2 xs
(++) [4] xs
```
こうすれば，型注釈(どんな型を受け取ってどんな型を返すのかを明確にしたもの)の順に書けるので，わかりやすいかと思います．

# 代数的データ型をあつかう
Haskellで代数的データ型(列挙体や構造体のようなもの)を扱うことができます．
```haskell
data Color = Red | Green | Blue
data RGB = RGB Int Int Int
```
これはC言語で言うところの
```C
enum Color {Red, Green, Blue};
typedef struct{
 int r;
 int g;
 int b;
}RGB;
```
に相当します．Haskellは型やコンストラクタの命名は大文字から始めるという規則があります．講習会では代数的データ型を使ったRGBの色の値を出すようなプログラムを実装しました．まずはColorからRGBのそれぞれの値を取得する`toRGB`を実装します．
```haskell
toRGB :: Color -> RGB
toRGB Red = RGB 255 0 0
toRGB Green = RGB 0 255 0
toRGB Blue = RGB 0 0 255
toRGB _ = RGB 0 0 0
```
多言語のif文やswitch文を使うことなく，数学的な関数のようにかけるのはHaskellのいいところだと感じますね．1行目は関数の型注釈，2行目以降が変数ごとの返り値を表しています．こんなふうに，他のフィールド型と同様に扱うことができます．Colorにコンストラクタを追加した場合は新たに`toRGB`の行を1行追加するだけで新たに色の規定ができます．続いて`RGB`の値を`String`型の`"#xxxxxx"`で返す関数`showRGB`を実装します．
```haskell
showRGB :: RGB -> String
showRGB (RGB r g b) = printf "#%02x%02x%02x" r g b
```
`RGB`は()でくくってやる必要があります．こうしないと，型が違うぞと怒られたり，`RGB`の要素が足りないぞと怒られたりします．また，`printf`という関数は，明示的にライブラリを読む必要があります．`printf`は`Text.Printf`をインポートすることで使うことができます．

最後に`main`を用意した全体のコードを載せます．

```haskell
import Text.Printf

data Color = Red | Green | Blue
data RGB = RGB Int Int Int

toRGB :: Color -> RGB
toRGB Red = RGB 255 0 0
toRGB Green = RGB 0 255 0
toRGB Blue = RGB 0 0 255
toRGB _ = RGB 0 0 0

showRGB :: RGB -> String
showRGB (RGB r g b) = printf "#%02x%02x%02x" r g b

main :: IO ()
main = do
putStrLn $ showRGB $ toRGB Blue 
```
