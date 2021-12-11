---
title: Git仓库小记
top: false
cover: false
toc: true
mathjax: false
date: 2021-04-29 22:28:42
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E5%B0%81%E9%9D%A2/Git.jpg
coverImg: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E5%B0%81%E9%9D%A2/Git.jpg
password:
summary: Git学习
tags:
	Git
categories: Git
---

# Git仓库小记

## 1.关联远程仓库

- 打开Git bush输入：

  ```Git
  git remote add origin git@github.com:zhaotaogit/images.git  
  ```

  - ​	origin为仓库地址的重命名，后面的链接为仓库链接。

  >如果git remote add时出现fatal:remote origin already exists,表示origin这个名字已经有了。
  >
  >可以用Git remote -v 查看远程仓库信息。
  >
  >然后 git remote remove origin删除这个远程仓库
  >
  >origin职业仓库链接的别名，可以随便起

## 2.创建版本库并提交文件

- 初始化git本地仓库	
  - 通过执行git init命令在本地初始化一个本地仓库，会在文件夹中生成一个.git的隐藏文件
- 通过git status命令查看暂存区情况

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/20210620140151.png"/>

- 创建完文件查看再暂存区，会提示你用git add将文件添加到暂存区

- 通过git add path 命令添加文件到暂存区,path是文件路径

  - git add . 是将所有文件添加到暂存区

- 执行git commit命令将暂存区里的改动给提交到本地的版本库，一般使用时会加-m：

  - git commit -m “描述”,简单描述这次调教的语句。

  <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/git%E6%8E%A8%E9%80%81%E5%92%8C%E4%B8%8A%E4%BC%A0.png"/>



## 3.把本地仓库推送到远程仓库

- 第一次推送,把本地的main和远程的main分支关联起来：

  ```
  git push -u origin main
  ```

  - 第一次推送要加-u


- 若在网页版创建了一个仓库，第一次提交不上去的话，需要先合并远程仓库的内容,然后再重新提交

  ```python
  git pull --rebase origin main	# 合并远程内容到本地
  ```

  

- 非第一次推送

  ```Git
  git push origin main
  ```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/%E6%95%88%E6%9E%9C.png"/>

## 4.克隆远程仓库

- 在你想要克隆到的位置打开Git bash

  ```Git
  git clone 链接
  ```

  - 链接写自己仓库的链接，然后回到文件夹就看到远程仓库的文件已经下载到本地了。

## 5.把服务器仓库的更新拉到本地仓库中

```Git
git pull
```

## 6.创建分支并进入

- 创建main分支，其实仓库里默认就有main分支，可以创建其他分支。

```Git
git checkout -b main
```

# 7.删除本地分支

- 删除本地的master分支

  ```Git
  git branch -D master 
  ```

## 8.删除Github项目上的分支

- 删除Github项目上的mster分支

```Git
git push origin --delete master 
```



## 9.删除仓库

1. 进入要删除的仓库：

   <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/20210620135848.png"/>

2. 点击Settings：

   <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/20210620135914.png"/>

3. 拉倒页面最下面：

   <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/20210620135937.png"/>

4. 按照提示输入：

   <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Git%E7%AE%A1%E7%90%86/20210620140006.png"/>

即可删除！



# 10参考链接

## [1.远程分支----git pull和git push命令用法介绍](https://blog.csdn.net/qq_42780289/article/details/97804091?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&dist_request_id=1619705520604_31908&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)