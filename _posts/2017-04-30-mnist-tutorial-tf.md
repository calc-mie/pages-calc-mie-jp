---
layout: post
title: "Mnistチュートリアルをやってみた"
author: "naca_cyan13"
---

[](
TensorflowMnisttutorialをやってみた\
Tensorflowとは？\
Mnistとは？\
PlaceHolder、Variable\
使った学習モデルについて\
今後\
)

Tensorflowを使うにあたり、右も左もわからないのでとりあえずチュートリアルをこなしてまとめようという趣旨の記事です。間違いはどんどん下のDisqusで指摘してください。今回は初回、Mnistチュートリアルをやりました。

link : [MNIST For ML Beginners - Tensorflow](https://www.tensorflow.org/get_started/mnist/beginners)


# Tensorflowとは

データフローグラフを使って数値計算を実現するライブラリです。C++やpythonなどから使えます。
ニューラルネットワークなどの実装に用いられます。

# データフローグラフとは

Tensorflowでは、処理をノード、矢印をテンソル（値やベクトル、テンソル）の流れとして、数値計算を実現します。
例えば $(5+3)/2$ なら以下の図。


![(5+3)/2](../images/tensorflow_add.svg)

これをコードでやると

```python
from tensorflow.examples.tutorials.mnist import input_data
import tensorflow as tf

def x_plus_y_div_z(x, y, z):
    _x = tensorflow.constant(x)
    _y = tensorflow.constant(y)
    add = tensorflow.add(_x, _y)
    div = tensorflow.div(add, tf.constant(z))
    return div

with tensorflow.Session() as sess:
    print(sess.run([x_plus_y_div_z(5, 3, 2)]))
```

のような感じ。

# Mnistとは

手書き文字を認識する機械学習プログラムのことです。Tensorflowの最初のTutorialとしてこれが用意されており、機械学習のHello,World的なものだそうです。

Mnistでは28x28pixelの画像を扱います。Tutorialでは28x28=784要素のベクトルとして画像一個をとらえています。TensorflowではMnistに使う画像データを取得する関数が用意されています。これを使ってデータを取り寄せます。

# 回帰モデル

Mnistチュートリアルではソフトマックス回帰(softmax regression)という方法で画像の推定を行います。(あんまりよくわかってないので後ほど調べる。)

概要は以下の式。

$$ \mathrm{softmax}:\mathbb{R}^{784} \rightarrow \mathbb{R}^{10}, \mathrm{softmax}(x) = \mathrm{normalize}(\mathrm{exp}(x)) $$
$$ y = \mathrm{softmax}(Wx + b) $$

この時、$W : \mathbb{R}^{784 \times 10}$はニューラルネットワークのウェイトの行列、$b : \mathbb{R}^{10}$はバイアスベクトルです。
$y$がこのモデルの順伝播の出力になります。

## PlaceHolderとVariable

モデルの値の管理のためにTensorflowでは2種類の変数形式が用意されています。

入力ベクトル$x$など伝播毎に代わる値は`tensorflow.placeholder`でモデルに流します。

```python
#784 dimention vector x defined as input 
x = tensorflow.placeholder(tf.float32, [None, 784])
```

逆にネットワークのウェイトやバイアスなどのモデルのパラメータなどは`tensorflow.Variable`でモデルに埋め込みます。


```python
#Weights from input to output 
W = tensorflow.Variable(tf.zeros([784,10]))
#biases
b = tensorflow.Variable(tf.zeros([10]))
```

これから最終的な出力$y$以下のコードで表現されます。

```python
y = tensorflow.nn.softmax(tf.matmul(x,W) + b)
```


# 学習

Mnistチュートリアルでは交差エントロピーを誤差関数として使います。交差エントロピーは確率分布の一致度を測定するために使われる関数です(今回は離散分布としてみなされてる)。二乗誤差なども誤差関数として使えるそうですが、交差エントロピーの方が収束が早いらしいです。（このへんも後ほど調べる）。正解出力$y'$に対する交差エントロピーの定義$\mathrm{H}_{y'}$は以下。

$$ \mathrm{H}_{y'} : \mathbb{R}^{10} \rightarrow \mathbb{R}, \mathrm{H}_{y'}(y) = - \sum_i^N y'_i \log(y_i) $$

これをもとにバックプロパゲーションします。


```python
cross_entropy = tensorflow.reduce_mean(
　   tensorflow.nn.softmax_cross_entropy_with_logits(labels=y_, logits=y))

train_step = tensorflow.train.GradientDescentOptimizer(0.5).minimize(cross_entropy)
```

tensorflowでは$\mathrm{softmax}$関数を計算してそこからクロスエントロピーをうんぬんとやるのは安定しないらしいです。かわりに`softmax_cross_entropy_with_logits`を使ってまとめてやってしまうようです。(以下引用)

>Note that in the source code, we don't use this formulation, because it is numerically unstable. Instead, we apply tf.nn.softmax_cross_entropy_with_logits

その下では、0.5の係数でモデルから勾配をとり最適化するOptimizerオブジェクトに、cross_entropyを出力するデータフローを食わせて最適化します。

# 結果

tutorialのページにも書いてありますが精度は`92%`弱という風になりました。

# TensorBoard(まだ未調査)

Tensorflowには学習の様子などを可視化するために、TensorBoardという機能が用意されています。これは他のライブラリにあまりない強力な機能で、学習係数やレイヤー数などハイパーパラメータの検討などに非常に有用な機能です。
プログラム側からログを吐きだし、TensorBoardというアプリケーションを走らせることによってそこにWebサーバーが立ち上がり、そこでいろいろな情報が表示されます。

# 今後

数理モデルがわからなさすぎるので

- 交差エントロピーの性質や意味
- Tensorflowでのバックプロパゲーション

をもっと調べたいと思います。TensorBoardのことやTensorflowのラッパーライブラリである**Keras**についても調べてみたいです。

# 参考文献

- [TensorFlowを算数で理解する - Qiita](http://qiita.com/icoxfog417/items/fb5c24e35a849f8e2c5d)
- [Tensorflow](https://www.tensorflow.org)
- [Neural Networkでの失敗経験やアンチパターンを語る](http://nonbiri-tereka.hatenablog.com/entry/2016/03/10/073633)


