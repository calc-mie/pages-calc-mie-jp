---
layout: post
title: "ランダウの記法"
author: "@naca_nyan"
---

## 定義
$x \to 0$ を考えるとき、 $f(x) = o(g(x))$ は、
$$\lim_{x \to 0} \frac{f(x)}{g(x)} = 0$$
を意味する。

$f(x)$ の $x \to 0$ での小さくなり方（$0$ への近づくはやさ）が $g(x)$ よりもはやい、という意味である。

## 例
以下、特に断らない限り $x \to 0$ を考える。

1. $$x^2 = o(x) \quad\quad \because \lim_{x \to 0} \frac{x^2}{x} = \lim_{x \to 0} x = 0$$
2. $$4x^3 + 5x^4 = o(x^2) \quad\quad \because \lim_{x \to 0} \frac{4x^3 + 5x^4}{x^2} = \lim_{x \to 0} (4x + 5x^2) = 0$$
3. $$x = o(e ^x) \quad\quad \because \lim_{x \to 0} \frac{x}{e^x} = \lim_{x \to 0} xe^{-x}= 0$$

$f(x) = h(x) + o(g(x))$ と書いたときは $f(x) - h(x) = o(g(x))$ と解釈する。

4. $$\cos(x) = 1 - \frac{x^2}{2} + o(x^3)$$
5. $$e^x = 1 + x + \frac {x^{2}}{2!}+\frac {x^{3}}{3!}+o(x^3)$$

## 注意
すこし不思議に思うかもしれないが、 $x = o(x)$ とはならない。実際
$$\lim_{x \to 0} \frac{x}{x} = 1 \ne 0$$
である。同様に、$f(x) = x + o(x)$ と $f(x) = o(x)$ は区別される。

## 性質
### (1)
$f(x) = o(g(x))$のとき、任意の定数$k$に対して$$kf(x) = o(g(x))$$である。
$$\because \lim_{x \to 0} \frac{kf(x)}{g(x)} = k \lim_{x \to 0} \frac{f(x)}{g(x)} = 0$$

### (2)
$f(x) = o(x^n)$のとき、$$x^mf(x) = o(x^{m+n})$$である。
$$\because \lim_{x \to 0} \frac{x^mf(x)}{x^{m+n}} = \lim_{x \to 0} \frac{f(x)}{x^n} = 0$$

### (3)
$f(x) = o(x^m), g(x) = o(x^n)$のとき、$$f(x)g(x) = o(x^{m+n})$$である。
$$\because \lim_{x \to 0} \frac{f(x)g(x)}{x^{m+n}} = \lim_{x \to 0} \frac{f(x)}{x^m}\frac{g(x)}{x^n} = 0$$

### (4)
$m \gt n, f(x) = o(x^n)$のとき、$$x^m + f(x) = o(x^{n})$$である。
$$\because \lim_{x \to 0} \frac{x^m + f(x)}{x^n} = \lim_{x \to 0} \left(x^{m-n} + \frac{f(x)}{x^n}\right) = 0$$

### (5)
$m \ge n, f(x) = o(x^m), g(x) = o(x^n)$のとき、$$f(x) + g(x) = o(x^{n})$$である。
$$\because \lim_{x \to 0} \frac{f(x) + g(x)}{x^n} = \lim_{x \to 0} \left(\frac{f(x)}{x^n} + \frac{g(x)}{x^n}\right) = 0$$

### 略記
以上の性質を単に以下のように書く。

1. $k \cdot o(g(x)) = o(g(x))$ （任意の定数$k$に対して）
2. $x^mo(x^n) = o(x^{m+n})$
3. $o(x^m)o(x^n) = o(x^{m+n})$
4. $x^m + o(x^n) = o(x^n)$ （ただし $m \gt n$）
5. $o(x^m) + o(x^n) = o(x^n)$ （ただし $m \ge n$）

## さらに注意
定数倍で$k = -1$を考えると、$- o(x^m) = -1 \cdot o(x^m) = o(x^m)$であるので、
$$\begin{aligned}
o(x^m) - o(x^m) &= o(x^m) + o(x^m) \\
&= o(x^m)
\end{aligned}$$
となる。最後の式変形では性質(5)をつかった。$o(x^m) - o(x^m) = 0$としないよう注意すること。

## 計算例
$f(x) = 1 + x + o(x), g(x) = 1 - 2x + o(x)$のとき、
$$\begin{aligned}
xf(x) - g(x) &= x(1 + x + o(x)) - (1 - 2x + o(x)) \\
 &= x + x^2 + xo(x) - 1 + 2x + o(x) \\
 &= -1 + 3x + x^2 + o(x^2) + o(x) \\
 &= -1 + 3x + o(x)
\end{aligned}$$
と計算できる。実際、
$$\begin{aligned}
\lim_{x \to 0} \frac{xf(x) - g(x) - (-1 + 3x)}{x} &= \lim_{x \to 0}\left(\frac{xf(x) - x}{x} - \frac{g(x) - (1 - 2x)}{x}\right) \\
 &= \lim_{x \to 0}\left(\frac{xf(x) - x}{x} - x\right) - \lim_{x \to 0}\frac{g(x) - (1 - 2x)}{x} \\
 &= \lim_{x \to 0}\frac{xf(x) - x - x^2}{x} \\
 &= \lim_{x \to 0}x\cdot\frac{f(x) - (1 + x)}{x} \\
 &= 0
\end{aligned}$$
となって優勝する。

## まとめ
$\lim$の計算はたいがい厳しいので、ランダウの記号が使えると便利。
だが等号が普通の意味ではなく、間違いやすいので注意して使おう。
