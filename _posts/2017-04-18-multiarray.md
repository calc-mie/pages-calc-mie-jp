---
title: "多次元配列の変な話"
author: "@SKsan_9642_univ"
---

C言語の配列についてしゃべるよ。

```
int array[10][20];
int *x,*y;
```

こんなプログラムを考えるよ

```
x = array[2];
y = &array[2][0];
```

この2つの式について
