---
title: Python异常
top: true
cover: true
toc: true
mathjax: false
date: 2021-11-18 16:32:24
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/20211118163844.png
coverImg:
password:
summary: Python异常
tags:
  Python
categories: Python
---

# Python异常

## 01.异常的概念

- 程序运行时，如果Python解释器 **遇到 **一个错误，会停止程序的执行，并且提示一些错误信息，这就是 **异常**。
- **程序停止执行并且提示错误信息**，这个动作，我们通常称之为：**抛出(raise)异常**。

```python
num = int(input('请输入一个数字：'))  ## 让用户输入一个整数。
print(num) ## 打印。
```

​		正常输入整数是不会报错的，而用户输入的不是整数的话就会报错，针对这一情况，就需要异常语句来处理。当出现报错时，给出一定的提示！，通过 **异常捕获 **可以针对突发事件做集中的处理，从而保证程序的 **稳定性和健壮性。**



## 02 .异常的捕获

### 2.1简单捕获异常语法

``` python
try:
    尝试运行的代码
 except:
    出现错误运行的代码
```

### 2.2错误类型捕获

- 在程序运行时，可能会遇到**不同类型的异常**，并且需要 **针对不同类型的异常，做出不同的响应**，这个时候，就需要捕获错误类型了。

- 语法如下:

  ```python
  try:
      尝试运行的代码
  except 错误类型1：
      针对错误类型1执行的代码
  except 错误类型2：
      针对错误类型2执行的代码
  except Exception as result:
      print(f'未知错误{result}')
  ```

- 当python解释器 **抛出异常**时，最后一行错误信息的第一个单词，就是错误类型。

- 捕获未知错误,在程序开发时，会出现没有预料到的报错，这时候就可以使用**捕获未知错误**。

- 代码如下：

  ``` python
  except Exception as result:
      print(f'未知错误{result}')
  ```

  ### 2.3异常捕获的完整语法

```python
try:
    尝试运行的代码
except 错误类型1：
    针对错误类型1执行的代码
except 错误类型2：
    针对错误类型2执行的代码
except Exception as result:
    print(f'未知错误{result}')
else:
    没有错误才会执行的代码
finally:
    无论是否有异常，都会执行的代码
```

## 03.异常的传递

- 异常的传递  - - 当 **函数/方法** 执行 **出现异常**，会 **将异常传递** 给函数/方法 的 **调用一方**
- 如果 **传递到主程序**，仍然 **没有异常处理**， 程序才会被终止

> 提示

- 在开发中，可以在主函数中增加 **异常捕获**

- 而在主函数中调用的其他函数，只要出现异常，都会传递到主函数的 **异常捕获** 中

- 这样就不需要再代码中，增加大量的 **异常捕获**，能够保证代码的整洁

  

## 04.抛出 **raise** 异常

### 4.1应用场景

- 在开发中，除了 **代码执行出错**`Python`解释器会**抛出 **异常之外

- 还可以根据 **应用程序 特有的业务需求 主动抛出异常**

  **示例：**

- 提示用户 **输入密码**，如果 **长度少于8**，抛出**异常**

``` python
def input_password():
    password = input('请输入密码:')
    if len(password) >= 8:
        return password
    raise Exception('密码长度不够！')  # 主动抛出异常


try:
    input_password()
except Exception as result:  # 捕获异常
    print(result)  # 打印异常信息

```

