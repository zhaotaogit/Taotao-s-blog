---
title: Conda创建python环境
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-11 12:06:55
author:
img: https://ss3.baidu.com/9fo3dSag_xI4khGko9WTAnF6hhy/baike/pic/item/78310a55b319ebc45d5c45dc8e26cffc1e17164a.jpg
coverImg: https://ss3.baidu.com/9fo3dSag_xI4khGko9WTAnF6hhy/baike/pic/item/78310a55b319ebc45d5c45dc8e26cffc1e17164a.jpg
password:
summary:
  - Python
  - Linux
tags:
  - Python
  - Linux
categories: 
  - Python
  - Linux
---
# Cnda创建python环境

## 1 列出当前存在的环境

可以用以下命令罗列出当前已经创建的python虚拟环境

![3f878fc75ad84405bffa29a309238655.jpg](http://tva1.sinaimg.cn/large/007gOsxTgy1gvvfvtklcsj32yo1o0e2l.jpg)

[IMG]http://tva1.sinaimg.cn/large/007gOsxTgy1gvvfualuzgj32yo1o0e2l.jpg[/IMG]

```cpp
conda env list
```

罗列结果如下所示:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Album_Src/Conda_list.jpg"/>

左边是虚拟环境的名称，右边是其所在路径，带星号的表示是默认环境。

## 2 创建虚拟环境

可以用如下命令创建一个名字为my_py_env，python版本为3.6.2的虚拟环境。

```undefined
conda create -n my_py_env python=3.6.2
```

该方式创建的环境在默认路径下，可以通过以下方式指定路径：

```swift
conda create --prefix="D:\\my_python\\envs\\my_py_env"  python=3.6.3
```

其中"D:\my_python\envs\"是路径名，"my_py_env" 是环境名.

## 3 进入环境

```undefined
activate my_py_env
```

在windows系统cmd下通过以上命令即可进入my_py_env环境，如果在linux系统下，需要使用：

```bash
source activate my_py_env
```

## 4 退出环境

windows:

```undefined
deactivate
```

linux：

```bash
source deactivate
```

## 5 使用conda管理包

```undefined
conda install -n my_py_env package_name
conda uninstall -n my_py_env package_name
```

只需要在conda命令中通过 -n 显示指定python环境即可

## 6 删除环境

```csharp
conda remove -n my_py_env --all
```

