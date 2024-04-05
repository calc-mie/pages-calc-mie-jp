---
title: "math-logic"
author: "teo"
---

# 数理論理学　その２
前回に引き続き、分かりにくかったところを自分のメモ代わりとして書いていきます。前回同様参考にしていただいたり、間違った部分を直していただけると幸いです。
今回はLK法、LJ法についてです。

## 今回理解したこと。

### 記号の導入
まず記号の導入から入ります。

>　このLKでは$$A_1\,\cdots\ A_n\, \vdash \, B_1 \, \cdots \, B_n$$というもの（以下これを式と呼ぶ）が対象となる.(p50)

ここで「$\vdash$」は、左辺（$A_1 \, \cdots \, A_n$)の全てが成立するならば
右辺（$B_1 \, \cdots \, B_n$）のうちどれかが成り立つという意味があります。
また、$\, m=0\,$または$\, n=0\,$でも扱えます。LK、LJの証明図は複数の公理から始まります。
公理は「$A \, \vdash \, A$」と書きます。

また、論理式の有限列（$A_1 \, \cdots \, A_n$）を$\Gamma ,\, \Pi ,\, \Delta ,\, \Lambda$等で表します。

### 推論規則
次に推論規則を列挙していきます。

* 増：
    + 左：　$$\frac {\Gamma \, \vdash \, \Delta} {A, \, \Gamma \, \vdash \, \Delta}$$
    + 右：　$$\frac {\Gamma \, \vdash \, \Delta} {\Gamma \, \vdash \, \Delta, \, A}$$
* 減：
    + 左：　$$\frac{A, \, A, \, \Gamma \, \vdash \, \Delta} {A, \, \Gamma \, \vdash \, \Delta}$$
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A, \, A} {\Gamma \, \vdash \, \Delta, \, A}$$
* 換：
    + 左：　$$\frac{\Gamma, \, A, \, B, \, \Pi \, \vdash \, \Delta}{\Gamma, \, B, \, A, \, \Pi \, \vdash \, \Delta}$$　　　
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A, \, B, \, \Pi }{\Gamma \, \vdash \, \Delta, \, B, \, A, \, \Pi}$$
* 三段論法：
    + $$\frac{\Gamma, \, \vdash \, \Delta, \,A \quad A , \, \Pi \, \vdash \, \Lambda}{\Gamma, \, \Pi \, \vdash \, \Delta, \, \Lambda}$$
* $\lnot$導入
    + 左：　$$\frac{\Gamma \, \vdash \, \Lambda, \, A }{\lnot A, \, \Gamma \, \vdash \, \Lambda}$$
    + 右：　$$\frac{\Gamma, \, A \, \vdash \, \Lambda}{ \Gamma \, \vdash \, \Lambda , \, \lnot A}$$
* $\land$導入
    + 左：　$$\frac{A, \, \Gamma \, \vdash \, \Delta}{A \, \land \, B, \, \Gamma \, \vdash \, \Delta}\quad\text{または}\quad\frac{B, \, \Gamma \, \vdash \, \Delta}{A \, \land \, B, \, \Gamma \, \vdash \, \Delta}$$
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A \quad \Pi \, \vdash \, \Lambda, \, B}{\Gamma, \, \Pi, \, \vdash \, \Delta, \, \Lambda, \, A \, \land \, B}$$
* $\lor$導入
    + 左：　$$\frac{A, \, \Gamma \, \vdash \, \Delta \quad B, \, \Pi \, \vdash \, \Lambda}{A \, \lor \, B, \, \Gamma, \, \Pi \, \vdash \, \Delta, \, \Lambda}$$
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A}{\Gamma \, \vdash \, \Delta, \, A \, \lor \, B \, }\quad\text{または}\quad\frac{\Gamma \, \vdash \, \Delta, \, B}{\Gamma \, \vdash \, \Delta, \, A \, \lor \, B}$$
* $\Rightarrow$導入
    + 左：　$$\frac{\Gamma \, \vdash \, \Delta, \, A \quad B, \,\Pi \, \vdash \, \Lambda}{A  \Rightarrow B, \, \Gamma, \, \Pi \, \vdash \, \Delta, \, \Lambda}$$
    + 右：　$$\frac{A, \, \Gamma \, \vdash \, \Delta, \, B}{\Gamma \, \vdash \, \Delta,\, A \Rightarrow B}$$
* $\forall$導入
    + 左：　$$\frac{A[^a_t], \, \Gamma \, \vdash \, \Delta}{\forall x A[^a_x], \, \Gamma \, \vdash \, \Delta}$$
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A}{\Gamma \, \vdash \, \Delta, \, \forall x A[^a_x]}$$
      ※ただし、自由変数$\,a\,$は下式に現れない.
* $\exists$導入
    + 左：　$$\frac{A, \, \Gamma \, \vdash \, \Delta}{\exists x A[^a_x], \, \Gamma \, \vdash \, \Delta}$$
      ※ただし、自由変数$\,a\,$は下式に現れない.
    + 右：　$$\frac{\Gamma \, \vdash \, \Delta, \, A[^a_t]}{\Gamma \, \vdash \, \Delta, \, \exists x A[^a_x]}$$

> (p52)

ここで、「ただし、自由変数$\,a\,$は下式に現れない.」についてですが、
$\forall$-右については、$\forall x(x=0) \Rightarrow a=0$は成立しない、また$\exists$-左については、$a=0 \Rightarrow \exists x(x=0)$が成立しないので、それぞれ下式にあってはいけません。

### LK、LJの違い
LJは「$A_1\,\cdots\ A_n\, \vdash \, B_1 \, \cdots \, B_n$」について、$n=0$または$n=1$のみを扱うものです。
この二つの特徴的な違いは排中律と二重否定の除去を認めるかどうかです。

||LK|LJ|
|:---:|:---:|:---:|
|排中律|認める|認めない|
|二重否定の除去|認める|認めない|
|二重否定の導入|認める|**認める**|

## まとめ
同値変形や直説法、数学的帰納法等に加えて証明方法がまた一つ学べたので利用していこうと思います。~~また、タイピング速度も多少上がったと思います。~~
