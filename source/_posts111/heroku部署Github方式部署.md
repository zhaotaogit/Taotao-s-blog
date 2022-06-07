---
title: heroku部署Github方式部署
top: true
cover: true
toc: true
mathjax: false
date: 2021-12-10 20:53:32
author: ZhTap
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/python-heroku-github.jpg
coverImg: https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/python-heroku-github.jpg
password:
summary:
tags:
categories:
---

# Heroku部署Github方式部署

## 1.本地仓库

1. 我们用Flask做示例，先写一个Flask服务：

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "<h1>Hello World!</h1>"

if __name__ == '__main__':
    app.run()
```

2. 创建一个Procfile文件

里面内容为:web gunicorn app:app

3. 生成当前项目的requirements.txt
4. 创建一个runtime文件

里面内容为：python-3.10

## 2.Heroku部署

![image-20211121190224009](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121190224009.png)

![image-20211121190249742](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121190249742.png)

