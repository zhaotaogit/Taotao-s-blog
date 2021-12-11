---
title: Linux安装Anaconda3环境配置指南
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-16 22:12:04
author:
img: https://ss3.baidu.com/9fo3dSag_xI4khGko9WTAnF6hhy/baike/pic/item/78310a55b319ebc45d5c45dc8e26cffc1e17164a.jpg
coverImg: https://ss3.baidu.com/9fo3dSag_xI4khGko9WTAnF6hhy/baike/pic/item/78310a55b319ebc45d5c45dc8e26cffc1e17164a.jpg
password:
summary:
	- Anaconda
	- Linux
tags: 
	- Anaconda
	- Linux
categories: 
	- Anaconda
	- Linux
---

# Linux安装Anaconda3环境配置指南

## 1.添加jupyter环境变量

```linux
find -name jupyter		找jupyter的位置

vim /etc/profile		编辑文件

根据找到的位置,在最后一行添加,PATH后面跟的路径自行改变：
export PATH=$PATH:/root/anaconda3/bin 

source  /etc/profile/		 执行配置
```

## 2.修改配置文件

```linux
jupyter notebook --generate-config		生成配置文件

vim  /root/.jupyter/jupyter_notebook_config.py 		编辑配置文件

添加代码：
c.NotebookApp.ip = '*'		配置可以访问的ip为所有ip
c.NotebookApp.open_browser = False		配置不自动打开浏览器
c.NotebookApp.port = 8888		配置服务端口为888

jupyter notebook --allow-root&  开启服务，root用户需要加--allow-root，&代表在后台运行
```

