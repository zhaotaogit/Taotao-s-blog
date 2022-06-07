---
title: Python报错
top: false
cover: false
toc: true
mathjax: false
date: 2021-11-18 17:49:49
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/Error.jpg
coverImg:
password:
summary: Python报错
tags: Python
categories: Python
---

# Pythonq报错

## 1.check_hostname requires server_hostname解决

**报错的原因**：
这个其实跟选用的python版本的关系不大，主要原因是因为每次使用 pip install 命令下载插件的时候，下载的都是最新的版本，比如下载requests插件，它会自动的将依赖的urllib3这个插件也安装，然后依赖的插件版本太高，就导致了这个报错的问题。
所以说，一般遇到这种莫名其妙的问题的时候，可以先去看一下是不是插件的问题导致的，解决措施就是 将urllib3插件的版本降低就可·以，当然，直接在安装requests插件的时候，选择用低版本也可以解决这个问题。比如用下面的命令指定版本进行安装：

```shell
pip install requests==2.20
```

或者使用下面的命令降低版本：

```shell
pip install urllib3==1.25.8
```
