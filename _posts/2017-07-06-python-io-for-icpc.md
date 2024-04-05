---
layout: post
title: "Pythonで競技プログラミングをするための入出力の方法"
author: "D4prog"
---


**Disclaimer:** ICPC国内予選仕様です。速度/メモリの面でのパフォーマンスは考慮しません



## 入力編

一行の入力を受け付ける場合、こう書きます
```
input()
```
整数への変換は `int(s)` を使います
```
n = int(input())
```

<hr />

一行に空白文字区切りの複数の入力を受け付ける場合、こう書きます
```
a, b = input().split()
```

一行に複数の整数の入力を受け付ける場合、こう書きます
```
a, b = [int(w) for w in input().split()]
```


```python
line = input()
print("'" + line + "'")

words = line.split()
print(words)

integers = [int(w) for w in words]
print(integers)

a, b = integers
# a, b = [int(w) for w in input().split()]
print(a, b)
```

    6 9
    '6 9'
    ['6', '9']
    [6, 9]
    6 9



```python
N = int(input())
mat = []
for i in range(N):
    mat.append([int(w) for w in input().split()])
print(mat)
```

    3
    1 2 3
    4 5 6
    7 8 9
    [[1, 2, 3], [4, 5, 6], [7, 8, 9]]



```python
help(str.split)
```

    Help on method_descriptor:
    
    split(...)
        S.split(sep=None, maxsplit=-1) -> list of strings
        
        Return a list of the words in S, using sep as the
        delimiter string.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified or is None, any
        whitespace string is a separator and empty strings are
        removed from the result.
    


セパレータ `sep` を指定しないと空白文字区切りで返ってきます


```python
# リスト内包表記使わず書くとこんな感じ
list(map(int, input().split()))
```

    1 2 3
    [1, 2, 3]



## 出力編


```python
print("Hello world")
print(1, 2, 3)
print("%d, %d" % (1, 2))
print("{}: {} ({})".format("key", "value", 3))
```

    Hello world
    1 2 3
    1, 2
    key: value (3)


### 文字列のフォーマットに関して


```python
a, b = 1, 2
print("a: %d, b: %d" % (a, b))
# for >= 3.6
# print(f"a: {a}, b: {b}")
```

    a: 1, b: 2


なお、剰余演算も `%` を用います。別の演算に同じ記号を割り当てるのは悪い文明です。


```python
print(777 % (7 * 7))
```

    42


### 改行なしはどうやるの？


```python
for i in range(10):
    print("%d " % i, end='')
print()
```

    0 1 2 3 4 5 6 7 8 9 



```python
" ".join(map(str, range(10)))
```




    '0 1 2 3 4 5 6 7 8 9'




```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    



```python
print(1, 2, 3, 4, sep=",\t")
```

    1,	2,	3,	4



