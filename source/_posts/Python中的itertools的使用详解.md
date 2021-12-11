---
title: Python中的itertools的使用详解
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-03 22:22:25
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Python%E5%B0%81%E9%9D%A2/Python.jpg
coverImg: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Python%E5%B0%81%E9%9D%A2/Python.jpg
password: 
summary: Python学习
tags:
	Python
categories: Python
---
# Python中的itertools的使用详解

**1.无穷的迭代器**

1.1 count(start,[step])

count()接受两个参数

-  start:循环开始的数字
-  step:循环中的间隔


```python
from itertools import count
 
"""
无穷的迭代器 count()
"""
c = count(0, 2)
v = next(c)
while v < 10:
  v = next(c)
  print(v, end=',')
```

1.2 cycle()

cycle就是一while True，无限循环里面的数字。

```python
"""
无穷迭代器 cycle()
"""
from itertools import cycle
 
c = cycle('ABCD')
for i in range(10):
  print(next(c), end=',')
```

1.3 repeat(elem,[n])

重复迭代elem，n次

```python
"""
无穷迭代器 repeat()
"""
from itertools import repeat
 
r = repeat(1, 3)
for i in range(3):
  print(next(r), end=',')
```

**2. 迭代器**

2.1 accumulate(p,[func])

使用func的函数对迭代对象p进行累积。

```python
"""
迭代器 accumulate()
"""
from itertools import accumulate
 
test_list = [i for i in range(1, 11)]
for i in accumulate(test_list): # 默认是operator.add
  print(i, end=',')
print()
for i in accumulate(test_list, lambda x, y: x * y): # operator.mul
  print(i, end=',')

```

2.2 chain()

chain()中可以放多个迭代对象，然后一一迭代出来。

```python
"""
迭代器 chain()
"""
from itertools import chain
 
ch = chain([1, 2, 3], {4: 4, 5: 5}, {6, 7, 8}, (9,), [10, [11, 12]])
for i in ch:
  print(i)
```

2.3 chain.from_iterable()

跟chain不同的地方在于:

-  chain: 可以接受多个迭代对象
-  chain.from_iterable():可以接受一个可以产生迭代对象的迭代器

```python
"""
迭代器 chain.from_iterable()
"""
def gen_iterables():
  for i in range(10):
    yield range(i)
 
for i in chain.from_iterable(gen_iterables()):
  print(i)

```

2.4 compress(data,selectors)

这是就是看下这个就知道了s是selectors中的元素。
(d[0] if s[0]), (d[1] if s[1]), ...

```python
"""
迭代器 compress
"""
from itertools import compress
 
print(list(compress(['A', 'B', 'C', 'D'], [0, 1, 1, 1])))
```

2.5 dropwhile(pred,seq)

循环开始的条件是，直到遇到第一次不满足pred条件的情况，才开始遍历。

```python
"""
迭代器 dropwhile()
"""
from itertools import dropwhile
 
l = [1, 7, 6, 3, 8, 2, 10]
print(list(dropwhile(lambda x: x < 3, l)))
```

2.6 groupby

这个感觉挺有意思的，有点像sql中的group_by。可以对字符串，列表等进行分组。

返回键和，组里的内容

```python
from itertools import groupby
 
# 对字符串进行分组
for k, g in groupby('11111234567'):
  print(k, list(g))
d = {1: 1, 2: 2, 3: 2}
# 按照字典value来进行分组
for k, g in groupby(d, lambda x: d.get(x)):
  print(k, list(g))
```

2.7 islice
这个就是对迭代对象进行切割，不支持负数，有点像range(1,10,2)这种

```python
from itertools import islice
print(list(islice('ABCDEFG', 2,3, None)))
```

2.8 zip_longest

这个和zip很像，不同地方在于:

-  zip结束取决于里面最短的迭代对象
-  zip_longest结束取决于里面最长的迭代对象

```python
from itertools import zip_longest
 
for x,y in zip_longest([1,2,3],[1,2]):
  print(x,y)
for x,y in zip([1,2,3],[1,2]):
  print(x,y)
```

**排列组合迭代器**

3.1 product

相当于 嵌套的for

```python
"""
排列组合迭代器 product 嵌套的for
"""
from itertools import product
for i,j in product([1,2,3],[4,5]):
print(i,j)
```

3.2 permutations

全排列，比如输出123的全部情况。(1,2,3),(1,3,2)…

```python
from itertools import permutations
print(list(permutations('123')))
```

3.3 combinations(p,r)

从p中找出所有长度为r的排列情况… 有顺序

```python
from itertools import combinations
print(list(combinations([1,2,3],2)))
```

3.4 combinations_with_replacement()

从p中找出所有长度为r的排列情况，有顺序，但包括自身就是会重复的意思。

-  combinations_with_replacement(‘ABCD', 2)
-  AA AB AC AD BB BC BD CC CD DD

了解是了解了，就是用的时候不知道能不能想起来…

以上就是本文的全部内容，希望对大家的学习有所帮助，也希望大家多多支持服务器之家。

原文链接：https://blog.csdn.net/qq_36659627/article/details/103926495