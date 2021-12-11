---
title: Python-Pandas一些命令笔记-持续更新
top: false
cover: false
toc: true
mathjax: false
date: 2021-04-27 20:23:18
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Python%E5%B0%81%E9%9D%A2/Python.jpg
coverImg: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Python%E5%B0%81%E9%9D%A2/Python.jpg
password:
summary: Python学习
tags:
	Python
categories: Python
---
# Python-一些命令笔记-持续更新

## 1.[python的u,r,b分别什么意思？](https://www.cnblogs.com/young233/p/11195577.html)

我们经常在python当中看到以下内容：

```python
print(u'hi\thi\thi')
print(b'hi\thi\thi')
print(r'hi\thi\thi')
```

在其他语言里没见过类似的，所以特此记录：

### u: 表示unicode字符串，默认模式，里边的特殊字符会被识别。

```python
print(u'hi\thi\thi')
```

执行之后：
**hi hi hi**

### b: 表示二进制字符串，括号内的内容原样输出。

```python
print(b'hi\thi\thi')
```

执行之后：
**b'hi\thi\thi'**

### r：不转义字符串，要输出的内容原样输出。

```python
print(r'hi\thi\thi')
```

执行之后：
**hi\thi\thi**

## 2.[Pandas时间序列——date_range方法](https://blog.csdn.net/wzyaiwl/article/details/90693214?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161952249816780271560229%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=161952249816780271560229&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-90693214.first_rank_v2_pc_rank_v29&utm_term=date_range)

- ### 功能

  date_range()方法主要用于生成一系列特定的时间，我们可以自己设定开始、结束、周期数、时间间隔、时区等等。

  ### 语法

  ```python
  import pandas
  
  pandas.date_range(start=None, end=None, periods=None, freq='D', tz=None, normalize=False, name=None, closed=None, **kwargs)
  ```

  ### 参数说明

  - start、end

    开始时间、结束时间，可以是str格式，也可以是datetime对象或None。

  - periods

    生成的周期数，可以是整数或None。

  ```python
  In [54]: pd.date_range(start='1/1/2018', end='1/08/2018')
  Out[54]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05', '2018-01-06', '2018-01-07', '2018-01-08'],
                dtype='datetime64[ns]', freq='D')
   
  In [55]: pd.date_range(start='1/1/2018', periods=8)
  Out[55]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05', '2018-01-06', '2018-01-07', '2018-01-08'],
                dtype='datetime64[ns]', freq='D')
   
  In [56]: pd.date_range(end='1/1/2018', periods=8)
  Out[56]:
  DatetimeIndex(['2017-12-25', '2017-12-26', '2017-12-27', '2017-12-28',
                 '2017-12-29', '2017-12-30', '2017-12-31', '2018-01-01'],
                dtype='datetime64[ns]', freq='D')
   
  In [57]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=3)
  Out[57]:
  DatetimeIndex(['2018-04-24 00:00:00', '2018-04-25 12:00:00',
                 '2018-04-27 00:00:00'],
                dtype='datetime64[ns]', freq=None)
   
  In [58]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=4)
  Out[58]: DatetimeIndex(['2018-04-24', '2018-04-25', '2018-04-26', '2018-04-27'], dtype='datetime64[ns]', freq=None)
   
  In [59]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=2)
  Out[59]: DatetimeIndex(['2018-04-24', '2018-04-27'], dtype='datetime64[ns]', freq=None)
   
  In [60]: pd.date_range(start='2018-04-24', end='2018-04-27', periods=5)
  Out[60]:
  DatetimeIndex(['2018-04-24 00:00:00', '2018-04-24 18:00:00',
                 '2018-04-25 12:00:00', '2018-04-26 06:00:00',
                 '2018-04-27 00:00:00'],
                dtype='datetime64[ns]', freq=None)
  ```

  - freq

    日期偏移量，即相邻时间的间隔，可以是str形式或DateOffset，默认为’D‘。

  ```python
  In [66]: pd.date_range(start='1/1/2018', periods=5, freq='5D')
  Out[66]:
  DatetimeIndex(['2018-01-01', '2018-01-06', '2018-01-11', '2018-01-16',
                 '2018-01-21'],
                dtype='datetime64[ns]', freq='5D')
   
  In [67]: pd.date_range(start='1/1/2018', periods=5, freq='M')
  Out[67]:
  DatetimeIndex(['2018-01-31', '2018-02-28', '2018-03-31', '2018-04-30',
                 '2018-05-31'],
                dtype='datetime64[ns]', freq='M')
   
  In [68]: pd.date_range(start='1/1/2018', periods=5, freq='H')
  Out[68]:
  DatetimeIndex(['2018-01-01 00:00:00', '2018-01-01 01:00:00',
                 '2018-01-01 02:00:00', '2018-01-01 03:00:00',
                 '2018-01-01 04:00:00'],
                dtype='datetime64[ns]', freq='H')
   
  In [69]: pd.date_range(start='1/1/2018', periods=5, freq=pd.offsets.MonthEnd(3))
  Out[69]:
  DatetimeIndex(['2018-01-31', '2018-04-30', '2018-07-31', '2018-10-31',
                 '2019-01-31'],
                dtype='datetime64[ns]', freq='3M')
  ```

  - tz

    设定时区，可以为str格式或tz fo。

  ```ruby
  In [70]: pd.date_range(start='1/1/2018', periods=5, tz='Asia/Tokyo')
  Out[70]:
  DatetimeIndex(['2018-01-01 00:00:00+09:00', '2018-01-02 00:00:00+09:00',
                 '2018-01-03 00:00:00+09:00', '2018-01-04 00:00:00+09:00',
                 '2018-01-05 00:00:00+09:00'],
                dtype='datetime64[ns, Asia/Tokyo]', freq='D')
   
  In [71]: pd.date_range(start='1/1/2018', periods=5, tz='Asia/Shanghai')
  Out[71]:
  DatetimeIndex(['2018-01-01 00:00:00+08:00', '2018-01-02 00:00:00+08:00',
                 '2018-01-03 00:00:00+08:00', '2018-01-04 00:00:00+08:00',
                 '2018-01-05 00:00:00+08:00'],
                dtype='datetime64[ns, Asia/Shanghai]', freq='D')
  ```

  - normalize

    布尔值，默认为False，若参数为True表示将start、end参数值正则化到午夜时间戳；

  ```python
  In [83]: pd.date_range(start='1/1/2018 14:00:00', periods=5,normalize=False)
  Out[83]:
  DatetimeIndex(['2018-01-01 14:00:00', '2018-01-02 14:00:00',
                 '2018-01-03 14:00:00', '2018-01-04 14:00:00',
                 '2018-01-05 14:00:00'],
                dtype='datetime64[ns]', freq='D')
   
  In [84]: pd.date_range(start='1/1/2018 14:00:00', periods=5,normalize=True)
  Out[84]:
  DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                 '2018-01-05'],
                dtype='datetime64[ns]', freq='D')
  ```

  - name

    生成时间索引对象的名称，取值为str g或None；

  ```python
  In [79]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None,freq='2D',name='xiaowoniu')
  Out[79]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', name=u'xiaowoniu', freq='2D')
  ```

  - closed

    若closed=’left’表示在返回的结果基础上，再取左闭右开的结果，若closed=’right’表示在返回的结果基础上，再取左开右闭的结果。当freq参数不为‘D’时，始终去掉的是为‘D‘时最左或最有的日期。

  ```python
  In [72]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None)
  Out[72]: DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
   
  In [73]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='left')
  Out[73]: DatetimeIndex(['2017-01-01', '2017-01-02', '2017-01-03'], dtype='datetime64[ns]', freq='D')
   
  In [74]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='right')
  Out[74]: DatetimeIndex(['2017-01-02', '2017-01-03', '2017-01-04'], dtype='datetime64[ns]', freq='D')
   
  In [75]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='right',freq='2D')
  Out[75]: DatetimeIndex(['2017-01-03'], dtype='datetime64[ns]', freq='2D')
   
  In [76]: pd.date_range(start='2017-01-01', end='2017-01-04', closed='left',freq='2D')
  Out[76]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', freq='2D')
   
  In [77]: pd.date_range(start='2017-01-01', end='2017-01-04', closed=None,freq='2D')
  Out[77]: DatetimeIndex(['2017-01-01', '2017-01-03'], dtype='datetime64[ns]', freq='2D')
  ```

  ## 3.[Python 数据清洗之缺失数据填充fillna()](https://blog.csdn.net/qq_21840201/article/details/81008566?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161960912416780261984422%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=161960912416780261984422&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-81008566.first_rank_v2_pc_rank_v29&utm_term=fillna)
  
  - 缺失数据比较多的情况下，可以直接滤除，缺失数据比较少时，对数据进行填充就很有必要了。
  - 数据填充函数fillna（）默认参数如下：
  
  - - 
  
  ```python
  import numpy as np
  from numpy import nan
  import pandas as pd
  data=pd.DataFrame(np.arange(3,19,1).reshape(4,4),index=list('abcd'))
  print(data)
  data.iloc[0:2,0:3]=nan
  print(data)
  
        0     1     2   3
  a   NaN   NaN   NaN   6
  b   NaN   NaN   NaN  10
  c  11.0  12.0  13.0  14
  d  15.0  16.0  17.0  18
  ```
  
  ``` python
  print(data.fillna(0))   ### 用0填充缺失数据
  
       0     1     2   3
  a  13.0  14.0  15.0   6
  b  13.0  14.0  15.0  10
  c  11.0  12.0  13.0  14
  d  15.0  16.0  17.0  18
  ```
  
  ```python
  print(data.fillna(method='bfill'))   ### 用相邻后面（back）特征填充前面空值
  
        0     1     2   3
  a  11.0  12.0  13.0   6
  b  11.0  12.0  13.0  10
  c  11.0  12.0  13.0  14
  d  15.0  16.0  17.0  18
  ```
  
  ``` python
  data=pd.DataFrame(np.arange(3,19,1).reshape(4,4),index=list('abcd'))
  data.iloc[1:2,:]=nan
  print(data)
  
       0     1     2     3
  a   3.0   4.0   5.0   6.0
  b   NaN   NaN   NaN   NaN
  c  11.0  12.0  13.0  14.0
  d  15.0  16.0  17.0  18.0
  ```
  
  ```python
  print(data.fillna(method='bfill'))   ### 用相邻前面（before）特征填充后面空值 
  
        0     1     2     3
  a   3.0   4.0   5.0   6.0
  b   3.0   4.0   5.0   6.0
  c  11.0  12.0  13.0  14.0
  d  15.0  16.0  17.0  18.0
  ```
  
  ```python
  values={0:10,1:20,2:30}
  print(data.fillna(value=values))   ### 用字典对不同的列填充不同的缺失数据
  
        0     1     2   3
  a  10.0  20.0  30.0   6
  b  10.0  20.0  30.0  10
  c  11.0  12.0  13.0  14
  d  15.0  16.0  17.0  18
  ```
  
  
