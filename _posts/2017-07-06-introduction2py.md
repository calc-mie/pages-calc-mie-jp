---
layout: post
title: "Introduction to Python"
author: "D4prog"
---


~~最悪、依存パッケージから何からユーザーインストールしなくてはいけないかと戦々恐々としていたのですが、~~  
Python3.5とJupyterが入ってたので諸々が楽です。


```python
#### HelloWorld
print("Hello World")
```

    Hello World



```python
#### 変数定義
a_variable = 1

print(a_variable)
```

    1



```python
#### 入力
line = input()
n = int(input())
f = float(input())
```

    line
    1
    3.14



```python
#### 変数の代入
first, last = 1, 2
# [first, last] とも書ける
print(first, last)

a, b, c = 1, 2, 3

max_, min_ = reversed([first, last])
# [max_, min_] とも書ける
print(min_, max_)
```

    1 2
    1 2



```python
#### 演算
print(1 + 2)
print(3 - 4)
print(5 * 6)
print(10 / 3)
print(10 // 3)
print(3 ** 3)
print(777 % (7 * 7))
print(hex(0xFF & 0x0F))
print(hex(0x0F | 0xF0))
print(bin(0x88 ^ 0xFF))
print(~0)
print(not True)
print(a < b and b < c)
```

    3
    -1
    30
    3.3333333333333335
    3
    27
    42
    0xf
    0xff
    0b1110111
    -1
    False
    True



```python
#### if 文
a, b = 1, 1
if a == b:
    print("a == b")
else:
    print("a != b")
```

    a == b



```python
#### elif
if a == b:
    pass
else:
    if a > b:
        pass

if a == b:
    pass
elif a > b:
    pass
else:
    pass

```


```python
# ソートする
a = [3, 2, 1]
print(sorted(a))

print(a)

a.sort()
print(a)
```

    [1, 2, 3]
    [3, 2, 1]
    [1, 2, 3]



```python
max_ = max(1, 2)
print(max_)
```

    2



```python
# 空白区切りで出力する
# (改行しないprint)

N = 3
for i in range(1, N+1):
    print(i, end='')
    if i < N:
        print(' ', end='')
print()

print(" ".join([str(i) for i in range(1, N+1)]))

a, b, c = 1, 2, 3
print(a, b, c, sep=' ')
```

    1 2 3
    1 2 3
    1 2 3



```python
#### for文と、一定回数のループ、range
for i in range(N):
    print(i)

print()

for i in range(1, N+1):
    print(i)

help(range)
```

    0
    1
    2
    
    1
    2
    3
    Help on class range in module builtins:
    
    class range(object)
     |  range(stop) -> range object
     |  range(start, stop[, step]) -> range object
     |  
     |  Return an object that produces a sequence of integers from start (inclusive)
     |  to stop (exclusive) by step.  range(i, j) produces i, i+1, i+2, ..., j-1.
     |  start defaults to 0, and stop is omitted!  range(4) produces 0, 1, 2, 3.
     |  These are exactly the valid indices for a list of 4 elements.
     |  When step is given, it specifies the increment (or decrement).
     |  
     |  Methods defined here:
     |  
     |  __contains__(self, key, /)
     |      Return key in self.
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(self, key, /)
     |      Return self[key].
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __reduce__(...)
     |      helper for pickle
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __reversed__(...)
     |      Return a reverse iterator.
     |  
     |  count(...)
     |      rangeobject.count(value) -> integer -- return number of occurrences of value
     |  
     |  index(...)
     |      rangeobject.index(value, [start, [stop]]) -> integer -- return index of value.
     |      Raise ValueError if the value is not present.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  start
     |  
     |  step
     |  
     |  stop
    



```python
#### 文字列のフォーマット
print("Case %d: %d" % (1, 10))
```

    Case 1: 10



```python
#### リスト内包表記


_2d6 = [(a, b) for a in range(1, 6+1) for b in range(1, 6+1)]
#print("\n".join(["%d: (%d, %d)" % (a+b, a, b) for a, b in _2d6]))
print(len(_2d6))


```

    36



```python
a, b, c = [int(w) for w in input().split()]
print(len([i for i in range(a, b+1) if c % i == 0]))
```

    5 14 80
    3



```python
#### ついでにセット内包表記
{c, c, c, a, b}
```




    {1, 2, 3}




```python
#### 使うか知らないけどついでに辞書
{"key_%d" % i: i for i in range(3)}
```




    {'key_0': 0, 'key_1': 1, 'key_2': 2}




```python
スライス

```


```python
enumerate
```


```python
a, b, c = 1, 2, 3
a < b < c
```




    True




```python
#### 関数と変数のスコープ

def a_function():
    a = 2
    b = 21
    if a < b: # if はスコープを作らない
        n = a * b
    else:
        n = a / b
    print(n)

a_function()
# print(n)  # NameError: name 'n' is not defined
# 関数はスコープを作る

for i in range(10): # for はスコープを作る
    pass
print(i)

lines = """Multi
Line
Text""".split("\n")

[line.upper() for line in lines]
# print(line)   # NameError: name 'line' is not defined
# リスト内包表記はスコープを作る

```

    42
    9





    ['MULTI', 'LINE', 'TEXT']




```python
# 真偽値と、三項演算子に関すること

True    # 真偽値は最初が大文字
False
while True:
    break

max_, n = 0, 10
max_ = max_ if max_ > n else n

```


```python
for i in range(10)[0:-1:2]: print(i)
```

    0
    2
    4
    6
    8



```python
3**3
```




    27




```python
import math
print(math.e, math.pi)

from cmath import isclose
print(isclose(math.e**(complex(0, 1)*math.pi) + 1, 0, abs_tol=1e-15))
```

    2.718281828459045 3.141592653589793
    True



```python
help(math.isclose)
```

    Help on built-in function isclose in module math:
    
    isclose(...)
        isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0) -> bool
        
        Determine whether two floating point numbers are close in value.
        
           rel_tol
               maximum difference for being considered "close", relative to the
               magnitude of the input values
            abs_tol
               maximum difference for being considered "close", regardless of the
               magnitude of the input values
        
        Return True if a is close in value to b, and False otherwise.
        
        For the values to be considered close, the difference between them
        must be smaller than at least one of the tolerances.
        
        -inf, inf and NaN behave similarly to the IEEE 754 Standard.  That
        is, NaN is not close to anything, even itself.  inf and -inf are
        only close to themselves.
    



```python
sum(range(1, 10+1))
```




    55



see also pep8

