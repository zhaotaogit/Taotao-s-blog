---
title: Flask入门
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-31 17:50:40
author:
img:
coverImg:
password:
summary:
tags:
categories:
---


# Flask入门-基于Ubuntu+Py3.85环境

- 调试命令

  > export FLASK_ENV=development		# 打开调试模式
  >
  > flask run --host=0.0.0.0		# 设置运行后，所有主机可见

- pycharm设置调试

  >app.run(debug=True)
  >
  >

## 一、创建虚拟环境&激活虚拟环境&安装Flask

> ## 虚拟环境
>
> 建议在开发环境和生产环境下都使用虚拟环境来管理项目的依赖。
>
> 为什么要使用虚拟环境？随着你的 Python 项目越来越多，你会发现不同的项目会需要 不同的版本的 Python 库。同一个 Python 库的不同版本可能不兼容。
>
> 虚拟环境可以为每一个项目安装独立的 Python 库，这样就可以隔离不同项目之间的 Python 库，也可以隔离项目与操作系统之间的 Python 库。
>
> Python 3 内置了用于创建虚拟环境的 [`venv`](https://docs.python.org/3/library/venv.html#module-venv) 模块。如果你使用的是较新的 Python 版本，那么请接着阅读本文下面的内容。
>
> 如果你使用 Python 2 ，请首先参阅 [安装 virtualenv](https://dormousehole.readthedocs.io/en/latest/installation.html#install-install-virtualenv) 。

### 1.创建虚拟环境

```she
mkdir myproject			# 创建一个文件
cd myproject			# 进入这个文件
python3 -m venv venv			# 创建一个名叫venv的虚拟环境
```

### 2.激活虚拟环境

在myproject文件夹下执行:

```shell
. venv/bin/activate
```

激活后，你的终端提示符会显示虚拟环境的名称。

### 3.安装Flask

在已激活的虚拟环境中可以使用如下命令安装 Flask：

```shell
pip install Flask
```



##  二、requirements文件的使用

### 1.导出环境所使用的所有模块名和版本号

```she
pip freeze > requirements.txt		# requirements.txt这个文件名可以自定义。
```

- 创建一个Flask项目，选好虚拟环境，随便创建一个程序，然后在终端执行代码

- 即可导出这个虚拟环境所使用的所有模块和版本号。

### 2.查看虚拟环境安装了那些模块

```she
pip list
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521215350134.png"/>

### 3.批量导入别的虚拟环境中的所有模块

- 即将一个虚拟环境里所有安装的模块安装到指定的环境中。

```shell
pip install -r requirements.txt			# requirements.txt	这个代表包含模块和版本号的文本文件。
```

执行命令之后，会将requirements.txt中所有的模块依次安装。

## 三、创建第一个Flask程序

### 1.Flask第一个程序

```python
from flask import Flask			# 导入Flask模块

app = Flask(__name__)

@app.route('/')		
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()			
```

运行结果:

```python
FLASK_APP = app.py
FLASK_ENV = development
FLASK_DEBUG = 0
In folder /Python/Flask
/Python/myproject/venv/bin/python3 -m flask run
 * Serving Flask app 'app.py' (lazy loading)
 * Environment: development
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521211157142.png"/>

此时点击Running on http://127.0.0.1:5000会跳转到浏览器，浏览器显示即：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521211507137.png"/>

和函数hello_world的返回结果是一样的。

### 2.代码详解

```python
from flask import Flask			# 导入Flask模块

# 创建Flask应用程序实例
app = Flask(__name__)			# 需要传入__name__,为了确定资源所在的路径。--后面会有具体解释

# 定义路由及视图函数
# Flask中定义路由是通过装饰器实现的。
@app.route('/')			# '/'代表根目录，即打开链接的第一界面。访问根路由会直接执行下面的函数。
def hello_world():
    return 'Hello, World!'

# 启动程序
if __name__ == '__main__':			# 判断__name__是否等于__main__
  	# 执行了app.run,就会将Flask程序运行在一个简易的服务器(Flask提供的，由于测试的。)
    app.run()			# 运行程序，
```

### 3.函数返回的形式

函数返回有2中形式：

- 一是上面代码中的return ‘Hello World’，即返回的是**字符串**。
- 二是返回一个**网页**。

**返回网页的方法**：

1. 在项目文件夹下的templates创建一个index.html的文件，里面的内容为你想在网页里显示出来的内容。

   <img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521214247102.png"/>

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <h1>Hello HTML5</h1>			<!--用一级标题显示'Hello HTML5'-->
   </body>
   </html>
   ```

   

2. 将from flask import Flask更改为from flask import Flask,render_template，其实就是多导入了一个templates。

```python
from flask import Flask,render_template
```



1. 然后将函数的返回代码改为return render_template('index.html')，括号里的内容为要显示的网页的文件名。

```HTML
def hello_world():    # return 'Hello World!'    return render_template('index.html')
```

完整程序代码：

```python
from flask import Flask,render_template

app = Flask(__name__)


@app.route('/')
def hello_world():
    # return 'Hello World!'
    return render_template('index.html')

if __name__ == '__main__':
    app.run()

```

运行结果：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521214541098.png"/>

## 四.路由请求方式设置

### 1.postman软件

- 直接官网下载然后打开，打开软件直接跳过，登录的下方有skip字样，点击就可以进入下图界面。

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521221146651.png"/>

- 试用软件发送get请求，查看返回结果。

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521221926274.png"/>

发现结果是正确的。

- 再用软件选择Post发送请求，查看返回结果。

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521221812412.png"/>

发现报了一个405的错误，即方法不允许，服务不支持post请求。

### 2.创建post请求

默认是Get请求,如果需要增加，需要自行指定。

将装饰器语句改成：

```python
@app.route('/',methods=['Get','Post'])
```

即加上请求方式参数，多个请求方式要用列表。

修改完成之后，再次发送post请求：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210521222629321.png"/>

发现并没有报错，和Get请求返回的结果是相同的，说明网页支持了Post请求了。



## 五、路由参数处理

### 1.同一个视图函数来显示不同用户的订单信息。

有时需要将同一类URL映射到同一个视图函数处理，比如:使用同一个视图函数来显示不同用户的订单信息。

```python
from flask import Flask,render_template

app = Flask(__name__)


@app.route('/',methods=['Get','Post'])
def hello_world():
    # return 'Hello World!'
    return render_template('index.html')

# 使用同一个视图函数来显示不同用户的订单信息。
# <>定义路由的参数。<>内需要起个名字,那么后面的代码才能使用。
@app.route('/orders/<order_id>')
def get_order_id(order_id):			# 需要在视图的()内填入参数名，那么后面的代码才能去使用。
    return 'order_id %s' % order_id

# 启动程序
if __name__ == '__main__':
    app.run()
```

上面的代码是在之前代码的基础上又定义了一个路由，目录为'/orders/<order_id>'，<>定义一个路由参数，<>内需要有个名字,代表动态目录。

上面代码运行后跟之前运行结果没有区别，但是在地址栏后面加上/orders/xxx,例如http://127.0.0.1:5000/orders/666

按F5刷新后的效果为:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522113029492-1624169288185.png"/>

可以发现显示内容为order_id 666,即get_order_id(order_id)函数的返回结果一致。

在get_order_id(order_id)函数中增加:print(order_id),然后运行程序，执行结果为：

```python
from flask import Flask,render_template

app = Flask(__name__)


@app.route('/',methods=['Get','Post'])
def hello_world():
    # return 'Hello World!'
    return render_template('index.html')

# 使用同一个视图函数来显示不同用户的订单信息。
# <>定义路由的参数。<>内需要起个名字,那么后面的代码才能使用。
@app.route('/orders/<order_id>')
def get_order_id(order_id):
    # 需要在视图的()内填入参数名，那么后面的代码才能去使用。
    print(type(order_id))
    return 'order_id %s' % order_id

# 启动程序
if __name__ == '__main__':
    app.run()
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522113621709.png"/>

可以看到打印出了<class ‘str’>，说明函数的参数order_id默认是一个字符串形式。

### 2.对路由做访问优化

有的时候，需要对路由做访问优化，订单ID应该是一个int类型。

所以我们将**@app.route('/orders/<order_id>')**修改为**@app.route('/orders/< int:order_id >')**,

即将order_id转化为int类型。当order_id可以转化为int类型时，就进行匹配，反之。此时，只有在http://127.0.0.1:5000/orders/xxx的xxx位置的参数是**可以转化为int类型**时，才会有返回结果，否则就是**Note Found**

举一反三:int也可以改成float等等

| `string` | （缺省值） 接受任何不包含斜杠的文本 |
| -------- | ----------------------------------- |
| `int`    | 接受正整数                          |
| `float`  | 接受正浮点数                        |
| `path`   | 类似 `string` ，但可以包含斜杠      |
| `uuid`   | 接受 UUID 字符串                    |



## 六、Jinja2模块引擎

><h1>模板</h1>
>
>视图函数的主要作用是生成请求的响应，这是最简单的请求。实际上，视图函数有两个作用：**处理业务逻辑**和**返回响应内容**。在大型应用中，把业务逻辑和表现内容放在一起，会增加代码的复杂度和维护成本。本节学到的模板，它的作用即是承担视图函数的另一个作用，即返回响应内容。
>
>- 模板其实是一个包含响应文本的文件，其中用占位符(变量)表示动态部分，告诉模板引擎其具体的值需要从使用的数据中获取
>- 使用真实值替换变量，再返回最终得到的字符串，这个过程称为“渲染”
>- Flask是使用 **Jinja2** 这个模板引擎来渲染模板
>
>使用模板的好处：
>
>- 视图函数只负责业务逻辑和数据处理(业务逻辑方面)
>- 而模板则取到视图函数的数据结果进行展示(视图展示方面)
>- 代码结构清晰，耦合度低

> <h1>Jinja2</h1>
>
> ### 两个概念：
>
> - Jinja2：是 Python 下一个被广泛应用的模板引擎，是由Python实现的模板语言，他的设计思想来源于 Django 的模板引擎，并扩展了其语法和一系列强大的功能，其是Flask内置的模板语言。
> - 模板语言：是一种被设计来自动生成文档的简单文本格式，在模板语言中，一般都会把一些变量传给模板，替换模板的特定位置上预先定义好的占位变量名。
>
> ### 渲染模版函数
>
> - Flask提供的 **render_template** 函数封装了该模板引擎
> - **render_template** 函数的第一个参数是模板的文件名，后面的参数都是键值对，表示模板中变量对应的真实值。



### 1.如何返回一个网页(模板)

- **这一部分在目录 三–3提过一次，但不详细**

> 创建完Flask项目后会生成2个文件夹static和templates,其中static可以将图片或者一些其他东西放进去，而templates就是用来放模板的。

1. 右键templates目录，新建一个HTML文件，随便写一些内容。

2. 然后导入模块from flask import Flask,render_template
3. 将函数返回结果设置为：**return render_template('index.html')**，其中**‘index.html’**为需要显示网页名,可自行修改。

Python代码：

```python
from flask import Flask,render_template

app = Flask(__name__)

# 1.如何返回一个网页(模板)
# 2.如何给模板填充数据
@app.route('/')
def hello_world():
    return render_template('index.html')


if __name__ == '__main__':
    app.run()
```

HTML代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
这个是模板<br>
这个是首页
</body>
</html>
```

运行结果:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522120929878.png"/>

可以看到显示的是网页的内容。

### 2.传入一个可变的东西

即在模板中不直接写死的东西：
```python
@app.route('/')
def hello_world():

    # 比如需要传入网址
    url_str = 'www.baidu.com'

    return render_template('index.html',url_str=url_str)			# 后面的参数为键值对的形式
```

==========================================================================
```htm
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
这个是模板<br>
这个是首页
{{ url_str }}<br>			# 加入了{{url_str}}
</body>
</html>
```

==========================================================================
**{% raw %}{# 注释内容 #}{% endraw %}是注释**
{% raw %}{{}}{% endraw %}是变量代码块
	
==========================================================================
<br>


运行结果：
<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522121806802.png"/>
- 当我们修改代码中的url_str的值时，网页内容也会发生改变。<br>



## 七、变量代码块的基本使用

### 1.数据的传递

 		代码 return render_template('index.html',url_str=url_str)中，前面一个url_str的意思是变量代码块要引用的名称，后面的url_str是py文件中的一个变量。通常模板中的变量名和传递数据的变量名保持一致。

python文件：

```python
from flask import Flask,render_template

app = Flask(__name__)

# 1.如何返回一个网页(模板)
# 2.如何给模板填充数据
@app.route('/')
def hello_world():

    # 比如需要传入网址
    url_str = 'www.baidu.com'
    my_list = [1,3,5,7,9]
    return render_template('index.html', url_str = url_str,my_list=my_list)


if __name__ == '__main__':
    app.run(Debug=True)

```


在html文件中：

```python
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
这个是模板<br>
这个是首页

{# 下面是一个变量代码快的使用#}
{{ url_str }}<br>
{{ my_list }}
</body>
</html>
```

运行结果:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522123039086.png"/>

可以看到在py文件中定义的my_list变量被传到了模板中并显示了出来。

### 2.列表数据传递

my_list是一个列表变量，同样，在模板中也可以使用切片

html代码：
```python
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
这个是模板<br>
这个是首页

{# 下面是一个变量代码快的使用#}
{{ url_str }}<br>
{{ my_list }}<br>
{{ my_list.2 }}			# 增加了这个
</body>
</html>
```
<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522123248935.png"/>

发现多了一个5

除了用点的方式，也可以使用同python切片[]的方式，有同样的效果。

### 3.字典数据的传递

除了列表，字典也可以

python：

```python
from flask import Flask,render_template

app = Flask(__name__)

# 1.如何返回一个网页(模板)
# 2.如何给模板填充数据
@app.route('/')
def hello_world():

    # 比如需要传入网址
    url_str = 'www.baidu.com'
    my_list = [1,3,5,7,9]
    my_dict = {
        'name':'赵涛涛',
        'age':18
    }
    return render_template('index.html', url_str = url_str,my_list=my_list,my_dict=my_dict)


if __name__ == '__main__':
    app.run(Debug=True)

```

html:
```python
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
这个是模板<br>
这个是首页

{# 下面是一个变量代码快的使用#}
{{ url_str }}<br>
{{ my_list }}<br>
{{ my_list.2 }}<br>
{{ my_dict }}<br>
{{ my_dict['name'] }}
</body>
</html>
```
运行结果:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522123853400.png"/>

发现字典也可以被正确的传递进来，还可以利用键取出值的方式。

**其他可以传递的数据不再赘述，自行探索**。



## 八、控制代码块

- 用{ %%}定义控制代码块，可以实现一些语言层次的功能，比如循环或者if语句。

```python
```python
{% if user %}
    {{ user }}
{% else %}
    hello!

{% for index in indexs %}
    {{ index }} 
{% endfor %}
```

- **快速补全技巧**

  先输入for然后按TAB键，即可快速补全。

  先输入if然后按TAB键，即可快速补全。

### 1.for语句

在html文件中增加：

```python
```html
{% for my in my_list %}
    {{ my }}<br>
{% endfor %}
```

再运行程序，发现网页依次打印出了my_list中的元素

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522125242127.png"/>

### 2.if语句

​	在刚刚的for语句修改为:
```python
```html
{% for my in my_list %}
    {% if my > 3 %}
        {{ my }}<br>
    {% endif %}
{% endfor %}
```

再运行程序，发现网页中只打印出了my_list中大于3的元素

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522125226237.png"/>

##  九、过滤器->叫转换器更好理解

### 1.概念及语法

过滤器的本质就是函数。有时候我们不仅仅只是需要输出变量的值，我们还需要修改变量的显示，甚至格式化、运算等等，而在模板中是不能直接调用 Python 中的某些方法，那么这就用到了过滤器。

使用方式：

- 过滤器的使用方式为：变量名 | 过滤器。

```python
```html
{{variable | filter_name(*args)}}
```

- 如果没有任何参数传给过滤器,则可以把括号省略掉

```python
```html
{{variable | filter_name}}
```

- 如{{ url_str | upper}}，这个过滤器的作用：把变量url_str 的值的所有小写字母转换为大写字母

  ​	{{ url_str | reverse}} 将字符串反转。

### 2.链式调用

在 jinja2 中，过滤器是可以支持链式调用的，示例如下：

```python
```html
{{ "hello world" | reverse | upper }}
```

**先反转再大写**

### 常见内建过滤器

### 字符串操作

- safe：禁用转义

```python
```html
<p>{{ '<em>hello</em>' | safe }}</p>
```

用了safe之后，<em></em>会直接应用到hello中，即把hello变成倾斜。

- capitalize：把变量值的首字母转成大写，其余字母转小写

```python
```html
<p>{{ 'hello' | capitalize }}</p>
```

- lower：把值转成小写

```python
```html
<p>{{ 'HELLO' | lower }}</p>
```

- upper：把值转成大写

```python
```html
<p>{{ 'hello' | upper }}</p>
```

- title：把值中的每个单词的首字母都转成大写

```python
```html
<p>{{ 'hello' | title }}</p>
```

- reverse：字符串反转

```python
```html
<p>{{ 'olleh' | reverse }}</p>
```

- format：格式化输出

```python
```html
<p>{{ '%s is %d' | format('name',17) }}</p>
```

- striptags：渲染之前把值中所有的HTML标签都删掉

```python
```html
<p>{{ '<em>hello</em>' | striptags }}</p>
```

- truncate: 字符串截断

```python
```html
<p>{{ 'hello every one' | truncate(9)}}</p>
```

### 列表操作

- first：取第一个元素

```python
```html
<p>{{ [1,2,3,4,5,6] | first }}</p>
```

- last：取最后一个元素

```python
```html
<p>{{ [1,2,3,4,5,6] | last }}</p>
```

- length：获取列表长度
```python
```html
<p>{{ [1,2,3,4,5,6] | length }}</p>
```

- sum：列表求和

```python
```html
<p>{{ [1,2,3,4,5,6] | sum }}</p>
```

- sort：列表排序

```python
```html
<p>{{ [6,2,3,1,5,4] | sort }}</p>
```

### 语句块过滤

```python
```html
{% filter upper %}
    一大堆文字
{% endfilter %}
```

## 十、Web表单

web表单是web应用程序的基本功能。

它是HTML页面中负责数据采集的部件。表单有三个部分组成：表单标签、表单域、表单按钮。表单允许用户输入数据，负责HTML页面数据采集，通过表单将用户输入的数据提交给服务器。

在Flask中，为了处理web表单，我们一般使用Flask-WTF扩展，它封装了WTForms，并且它有验证表单数据的功能

## WTForms支持的HTML标准字段

| 字段对象           | 说明                                      |
| :----------------- | :---------------------------------------- |
| StringField        | 文本字段                                  |
| TextAreaField      | 多行文本字段                              |
| PasswordField      | 密码文本字段                              |
| HiddenField        | 隐藏文件字段                              |
| DateField          | 文本字段，值为 datetime.date 文本格式     |
| DateTimeField      | 文本字段，值为 datetime.datetime 文本格式 |
| IntegerField       | 文本字段，值为整数                        |
| DecimalField       | 文本字段，值为decimal.Decimal             |
| FloatField         | 文本字段，值为浮点数                      |
| BooleanField       | 复选框，值为True 和 False                 |
| RadioField         | 一组单选框                                |
| SelectField        | 下拉列表                                  |
| SelectMutipleField | 下拉列表，可选择多个值                    |
| FileField          | 文件上传字段                              |
| SubmitField        | 表单提交按钮                              |
| FormField          | 把表单作为字段嵌入另一个表单              |
| FieldList          | 一组指定类型的字段                        |

## WTForms常用验证函数

| 验证函数     | 说明                                     |
| :----------- | :--------------------------------------- |
| DataRequired | 确保字段中有数据                         |
| EqualTo      | 比较两个字段的值，常用于比较两次密码输入 |
| Length       | 验证输入的字符串长度                     |
| NumberRange  | 验证输入的值在数字范围内                 |
| URL          | 验证URL                                  |
| AnyOf        | 验证输入值在可选列表中                   |
| NoneOf       | 验证输入值不在可选列表中                 |

使用Flask-WTF需要配置参数SECRET_KEY。

CSRF_ENABLED是为了CSRF（跨站请求伪造）保护。 SECRET_KEY用来生成加密令牌，当CSRF激活的时候，该设置会根据设置的密匙生成加密令牌。在HTML页面中直接写form表单：

### 1.使用普通方式实现表单

Python:

```python
from flask import Flask,render_template,request

app = Flask(__name__)

'''
实现一个简单的登录的逻辑处理
1.路由需要有get和post两种请求方式 --> 需要判断请求方式
2.获取请求参数
3.判断参数是否填写，以及密码是否相同
4.如果判断都没有问题，就返回一个succes
'''

@app.route('/',methods=['GET','POST'])
def index():
    # request:请求对象--> 获取请求方式、数据

    # 1.需要判断请求方式
    if request.method =='POST':
        # 2.获取请求参数
        username = request.form.get('username')
        passwprd = request.form.get('password')
        password2 = request.form.get('password2')
        print(username)
        # 3.判断参数是否填写 & 密码是否相同
        if not all([username,passwprd,password2]):
            print('参数不完整')
        elif passwprd !=password2:
            print('密码不一致')
        else:
            return 'succes'
    return render_template('index.html')


if __name__ == '__main__':
    app.run()
```

#### HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form method="post">
<form method="post">
    <label>用户名:</label><input type="text" name="username"><br>
    <label>密码:</label><input type="password" name="password"><br>
    <label>确认密码:</label><input type="password" name="password2"><br>
    <input type="submit" value="提交"><br>

</form>
</form>
</body>
</html>
```

当程序运行时，出现了一个表单，需要输入用户名、密码、确认密码，只有三者都不是空且密码和确认密码相同时才会返回succes，否则会打印错误。

### 2.提示优化

上面的程序运行后，当输入不正确的时候会提示错误，但是错误只显示在控制台，并没有在网页中提示，为了解决这个问题需要进行改进。

1. 导入flash：from flask import Flask,render_template,request,flash，并设置secret-key 
2. 将上放的print输出都改成flash输出
3. 在html文件表单中加入循环语句遍历消息

python代码

```python
from flask import Flask,render_template,request,flash

app = Flask(__name__)

app.secret_key = 'taotao'			# 设置secret_key

'''
实现一个简单的登录的逻辑处理
1.路由需要有get和post两种请求方式 --> 需要判断请求方式
2.获取请求参数
3.判断参数是否填写，以及密码是否相同
4.如果判断都没有问题，就返回一个succes
'''

'''
给模板传递消息
flash --> 需要对内容加密，因此需要设置secret_key,做一个加密消息的混淆
模板中需要遍历消息
'''

@app.route('/',methods=['GET','POST'])
def index():
    # request:请求对象--> 获取请求方式、数据

    # 1.需要判断请求方式
    if request.method =='POST':
        # 2.获取请求参数
        username = request.form.get('username')
        passwprd = request.form.get('password')
        password2 = request.form.get('password2')
        print(username)
        # 3.判断参数是否填写 & 密码是否相同
        if not all([username,passwprd,password2]):
            # print('参数不完整')
            flash('参数不完整！')
        elif passwprd !=password2:
            # print('密码不一致')
            flash('密码不一致')
        else:
            return 'succes'
    return render_template('index.html')


if __name__ == '__main__':
    app.run()

```

html代码

```Html
<!DOCTYPE html><html lang="en"><head>    <meta charset="UTF-8">    <title>Title</title></head><body><form method="post"><form method="post">    <label>用户名:</label><input type="text" name="username"><br>    <label>密码:</label><input type="password" name="password"><br>    <label>确认密码:</label><input type="password" name="password2"><br>    <input type="submit" value="提交"><br>    {#使用遍历获取闪现的消息#}    {% for message in get_flashed_messages() %} 			        {{ message }}    {% endfor %}</form></form></body></html>
```

get_flashed_messages()是一个函数，用于捕捉消息。	

程序运行后当输入参数不正确会在网页给予提示，如图：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210522153138471.png"/>

### 3.使用Flask_WTF实现表单

Python代码：

```python
from flask import Flask,render_template,request,flash
from flask_wtf import FlaskForm		# 导入模块
from wtforms import StringField,PasswordField,SubmitField

app = Flask(__name__)

app.secret_key = 'taotao'

'''
实现一个简单的登录的逻辑处理
1.路由需要有get和post两种请求方式 --> 需要判断请求方式
2.获取请求参数
3.判断参数是否填写，以及密码是否相同
4.如果判断都没有问题，就返回一个succes
'''

'''
给模板传递消息
flash --> 需要对内容加密，因此需要设置secret_key,做一个加密消息的混淆
模板中需要遍历消息
'''

'''
使用WTF实现表单
自定义表单类
'''

class LoginForm(FlaskForm):			# 继承FlaskFrom
    # 创建需要用到的对象
    username = StringField('用户名:')
    password = PasswordField('密码:')
    password2 = PasswordField('确认密码:')
    submit = SubmitField('提交')

# 创建一个路由，目录为‘/from’
@app.route('/form',methods = ['GET','POST'])
def login():
    login_form = LoginForm()
    return render_template('index.html',form = login_form)

@app.route('/',methods=['GET','POST'])
def index():
    # request:请求对象--> 获取请求方式、数据

    # 1.需要判断请求方式
    if request.method =='POST':
        # 2.获取请求参数
        username = request.form.get('username')
        passwprd = request.form.get('password')
        password2 = request.form.get('password2')
        print(username)
        # 3.判断参数是否填写 & 密码是否相同
        # validate_on_submit()需要CSRF token
        if not all([username,passwprd,password2]):
            # print('参数不完整')
            flash('参数不完整！')
        elif passwprd !=password2:
            # print('密码不一致')
            flash('密码不一致')
        else:
            return 'succes'
    return render_template('index.html')


if __name__ == '__main__':
    app.run()

```



html代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form method="post">
    <label>用户名:</label><input type="text" name="username"><br>
    <label>密码:</label><input type="password" name="password"><br>
    <label>确认密码:</label><input type="password" name="password2"><br>
    <input type="submit" value="提交"><br>

    {#使用遍历获取闪现的消息#}
    {% for message in get_flashed_messages() %}
        {{ message }}
    {% endfor %}
</form>
<hr>
<form method="post">
    {{ form.csrf_token() }}
    {{ form.username.label }}{{ form.username }}<br>
    {{ form.password.label }}{{ form.password }}<br>
    {{ form.password2.label }}{{ form.password2 }}<br>
    {{ form.submit }}

</form>
</form>
</body>
</html>
```

## 十一、Flask中使用数据库

### Flask-SQLAlchemy扩展

- SQLALchemy 实际上是对数据库的抽象，让开发者不用直接和 SQL 语句打交道，而是通过 Python 对象来操作数据库，在舍弃一些性能开销的同时，换来的是开发效率的较大提升
- SQLAlchemy是一个关系型数据库框架，它提供了高层的ORM和底层的原生数据库的操作。flask-sqlalchemy是一个简化了SQLAlchemy操作的flask扩展。

### 1.安装 flask-sqlalchemy

```
pip install flask-sqlalchemy
```

如果连接的是mysql数据库,需要安装mysqldb

```
pip install flask-mysqldb
```

#### #使用Flask-SQLAlchemy管理数据库

在Flask-SQLAlchemy中，数据库使用URL指定，而且程序使用的数据库必须保存到Flask配置对象的SQLALCHEMY_DATABASE_URI键中。

#### Flask的数据库设置：

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1:3306/test'
```

其他设置：

```python
# 动态追踪修改设置，如未设置只会提示警告, 不建议开启
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
# 查询时会显示原始SQL语句
app.config['SQLALCHEMY_ECHO'] = True
```

## 3.一些参数

| 名字                      | 备注                                                         |
| :------------------------ | :----------------------------------------------------------- |
| SQLALCHEMY_DATABASE_URI   | 用于连接的数据库 URI 。例如:sqlite:////tmp/test.dbmysql://username:password@server/db |
| SQLALCHEMY_BINDS          | 一个映射 binds 到连接 URI 的字典。更多 binds 的信息见[*用 Binds 操作多个数据库*](http://docs.jinkan.org/docs/flask-sqlalchemy/binds.html#binds)。 |
| SQLALCHEMY_ECHO           | 如果设置为Ture， SQLAlchemy 会记录所有 发给 stderr 的语句，这对调试有用。(打印sql语句) |
| SQLALCHEMY_RECORD_QUERIES | 可以用于显式地禁用或启用查询记录。查询记录 在调试或测试模式自动启用。更多信息见get_debug_queries()。 |
| SQLALCHEMY_NATIVE_UNICODE | 可以用于显式禁用原生 unicode 支持。当使用 不合适的指定无编码的数据库默认值时，这对于 一些数据库适配器是必须的（比如 Ubuntu 上 某些版本的 PostgreSQL ）。 |
| SQLALCHEMY_POOL_SIZE      | 数据库连接池的大小。默认是引擎默认值（通常 是 5 ）           |
| SQLALCHEMY_POOL_TIMEOUT   | 设定连接池的连接超时时间。默认是 10 。                       |
| SQLALCHEMY_POOL_RECYCLE   | 多少秒后自动回收连接。这对 MySQL 是必要的， 它默认移除闲置多于 8 小时的连接。注意如果 使用了 MySQL ， Flask-SQLALchemy 自动设定 这个值为 2 小时。 |

### 常用的SQLAlchemy字段类型

| 类型名       | python中类型      | 说明                                                |
| :----------- | :---------------- | :-------------------------------------------------- |
| Integer      | int               | 普通整数，一般是32位                                |
| SmallInteger | int               | 取值范围小的整数，一般是16位                        |
| BigInteger   | int或long         | 不限制精度的整数                                    |
| Float        | float             | 浮点数                                              |
| Numeric      | decimal.Decimal   | 普通整数，一般是32位                                |
| String       | str               | 变长字符串                                          |
| Text         | str               | 变长字符串，对较长或不限长度的字符串做了优化        |
| Unicode      | unicode           | 变长Unicode字符串                                   |
| UnicodeText  | unicode           | 变长Unicode字符串，对较长或不限长度的字符串做了优化 |
| Boolean      | bool              | 布尔值                                              |
| Date         | datetime.date     | 时间                                                |
| Time         | datetime.datetime | 日期和时间                                          |
| LargeBinary  | str               | 二进制文件                                          |

### 常用的SQLAlchemy列选项

| 选项名      | 说明                                              |
| :---------- | :------------------------------------------------ |
| primary_key | 如果为True，代表表的主键                          |
| unique      | 如果为True，代表这列不允许出现重复的值            |
| index       | 如果为True，为这列创建索引，提高查询效率          |
| nullable    | 如果为True，允许有空值，如果为False，不允许有空值 |
| default     | 为这列定义默认值                                  |

### 常用的SQLAlchemy关系选项

| 选项名         | 说明                                                         |
| :------------- | :----------------------------------------------------------- |
| backref        | 在关系的另一模型中添加反向引用                               |
| primary join   | 明确指定两个模型之间使用的联结条件                           |
| uselist        | 如果为False，不使用列表，而使用标量值                        |
| order_by       | 指定关系中记录的排序方式                                     |
| secondary      | 指定多对多中记录的排序方式                                   |
| secondary join | 在SQLAlchemy中无法自行决定时，指定多对多关系中的二级联结条件 |





## 十二、数据库的基本操作-环境改成了windows，因为遇到了问题，ubuntu环境折腾不好

- 将已经写好的python项目复制黏贴到windows上就好了，用pycharm以打开项目的方式打开文件夹。

## 一. 增删改操作

### 1. 基本概念

- 在Flask-SQLAlchemy中，插入、修改、删除操作，均由数据库会话管理。
  - 会话用db.session表示。在准备把数据写入数据库前，要先将数据添加到会话中然后调用 commit() 方法提交会话。
- 在Flask-SQLAlchemy中，查询操作是通过query对象操作数据。
  - 最基本的查询是返回表中所有数据，可以通过过滤器进行更精确的数据库查询。

### 2.在数据表中添加数据

**代码中有些生僻的参数，可以查询上一节的参数表。**

Python代码:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy


app = Flask(__name__)

# 配置数据的地址
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1/flask'
# 配置数据库是否动态追踪修改设置，如未设置只会提示警告, 不建议开启
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)


'''
两张表(管理员/普通用户)
角色(角色ID)
'''

# 数据库的模型，需要继承db.Model
class Role(db.Model):
    # 定义表名
    __tablename__ = 'roles'			# 表名
    # 定义字段
    # db.Column表示一个字段
    id = db.Column(db.Integer,primary_key=True)  # 主键
    name = db.Column(db.String(16),unique=True)

class User(db.Model):
    __tablename__ = 'users'			# 表名
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(16),unique=True)
    role_id = db.Column(db.Integer,db.ForeignKey('roles.id'))  # 表示是表roles的外键

@app.route('/')
def hello_world():
    return 'Hello World!'


if __name__ == '__main__':
    # 删除表
    db.drop_all()
    # 创建表
    db.create_all()
    app.run(debug=True)
```

运行这个程序，就可以在mysql中的flask这个库创建指定的两个数据表。在这个文件里创建了两个类，我们可以利用这两个类进行数据表的增加。

#### 注意事项

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1:3306/flask' 
这句代码是用来链接数据库，其中最前面的mysql是指定数据库类型，root是数据库的用户名，紧接着的mysql是数据库密码，@后面的是自己的地址，可以是127.0.0.1也可以是localhost，后面的端口号可以写也可以不写，最后flask是我们在mysql中创建的数据库。
```

运行最上面的代码前，需要在mysql中运行下列代码：

```mysql
create database flask 		# 创建flaks数据库
use flask		# 进入flask数据库
```

#### 一些后面要用到的代码

```mysql
show database;		# 查看有哪些数据库
show tables;		# 查看数据库下有哪些表
desc roles;		# 查看表中有哪些字段名及数据类型
select * from roles;		# 查询某个表中所有数据
```

**注意**：在mysql中写代码，每句代码结尾都要跟上‘；’分号。

然后再运行python代码，在mysql中执行show tables;代码效果如图：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210524171951262.png"/>

可以发现mysql中成功创建了两个表。

为了在表中添加数据，我们用pycharm自带终端/python控制台来添加数据:

推荐使用Python控制台，因为如果使用的是虚拟环境，终端输入ipython之后用的是base环境，不是虚拟环境，会导致报错，而python控制台本身就是虚拟环境下的ipython。

执行下列代码：

```python
from app from *			# 导入一个模块，其中app为py文件的名字
role  = Role(name = 'admin')		# 调用类，传入一个name参数
db.session.add(role)			# 添加到数据库的session中
db.session.commit()			#提交数据库的修改(包括增/删/改)
```

然后再mysql中执行select * from roles*,结果如图:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210524173231779.png"/>

可以发现在roles表中已经添加了一条数据。

接着我们在users表中添加如下数据：

```mysql
user = User(name = 'heima',role_id = role.id)		# 因为User中的role_id是Role中id的外键，role.id是取role对象的id，role的id默认生成了一个1。
db.session.add(user)		# 添加修改
db.session.commit()			# 提交修改
```

然后在mysql中执行:

```mysql
select * from users		# 查询users表
```

结果：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210524174008843.png"/>

成功添加了一条数据；

**方法汇总:**


```
db.session.add(role)    添加到数据库的session中db.session.add_all([user1, user2]) 添加多个信息到session中db.session.commit()     提交数据库的修改(包括增/删/改)db.session.rollback()   数据库的回滚操作db.session.delete(user) 删除数据库(需跟上commit)
```

### 3 修改数据表中的数据

- 以下步骤都是在上面步骤完成的情况下追加的。

```python
user.name = 'chengxuyuan'		# 将user对象的name改成‘chengxuyuan'db.session.commit()			# 直接提交，不需要add
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210524174812523.png"/>

### 4.删除数据表的中数据

```python
db.session.delete(user)			# 将user对象的name从数据表中删除db.session.commit()			# 直接提交
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210524174847453.png"/>

#### 5.**汇总**

```
#### 2.2 数据的增删改​```python# 进入ipython一次执行In [1]: from demo3_sqlalchemy import *# 添加一条Role数据In [2]: role = Role(name='admin')In [3]: db.session.add(role)In [4]: db.session.commit()# 添加一条User数据, 数据有误可以使用回滚, 将add的对象从session移除In [5]: user = User(name='zhangsan')In [6]: db.session.add(user)In [7]: db.session.rollback()In [9]: user.role_id = 1In [6]: db.session.add(user)In [4]: db.session.commit()# 修改数据In [13]: user.name = 'lisi'In [14]: db.session.commit()# 删除数据In [16]: db.session.delete(user)In [17]: db.session.commit()
```



## 二、模型之间的关联

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy


app = Flask(__name__)

# 配置数据的地址
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1/flask'
# 配置数据库是否动态追踪修改设置，如未设置只会提示警告, 不建议开启
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)


'''
两张表(管理员/普通用户)
角色(角色ID)
'''

# 数据库的模型，需要继承db.Model
class Role(db.Model):
    # 定义表名
    __tablename__ = 'roles'
    # 定义字段
    # db.Column表示一个字段
    id = db.Column(db.Integer,primary_key=True)  # 主键
    name = db.Column(db.String(16),unique=True)

    # 在一的一方，写关联。
    # users = db.relattionship('User'):表示和User模型发生了关联，增加了一个user属性
    # backref = 'role'：表示role是User要用的属性
    users = db.relationship('User', backref='role')


        def __repr__(self):
        return '\n<Role: %s %s>' % (self.name, self.id)

class User(db.Model):
    __tablename__ = 'users'
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(16),unique=True)
    email = db.Column(db.String(32),unique=True)
    password = db.Column(db.String(32))
    role_id = db.Column(db.Integer,db.ForeignKey('roles.id'))  # 表示是表roles的外键
    # User希望有role属性，但是这个属性的定义，需要在另一个模型中定义。

    def __repr__(self):
        return '\n<User: %s %s %s %s>' % (self.name, self.id, self.email, self.password)

@app.route('/')
def hello_world():
    return 'Hello World!'


if __name__ == '__main__':
    # 删除表
    db.drop_all()
    db.create_all()
    # 创建表
    app.run(debug=True)
```

python控制台

```python
from app import *
role = Role(name = 'admin')
db.session.add(role)
db.session.commit()
user1 = User(name = 'zs',role_id = role.id)
user2 = User(name = 'ls',role_id = role.id)
db.session.add_all([user1,user2])
db.session.commit()
role.users			# 通过role.users可以查到User中的数据信息
> [User: 1 zs 1 , User: 2 ls 1 ]
user1.role			# 通过user1.role可以查询出user1的Role信息
> Role: 1 admin 
user2.role
> Role: 1 admin 
```

## 三、查询操作

### 1. 基本概念

### 1.1 常用的SQLAlchemy查询过滤器

| 过滤器      | 说明                                             |
| :---------- | :----------------------------------------------- |
| filter()    | 把过滤器添加到原查询上，返回一个新查询           |
| filter_by() | 把等值过滤器添加到原查询上，返回一个新查询       |
| limit       | 使用指定的值限定原查询返回的结果                 |
| offset()    | 偏移原查询返回的结果，返回一个新查询             |
| order_by()  | 根据指定条件对原查询结果进行排序，返回一个新查询 |
| group_by()  | 根据指定条件对原查询结果进行分组，返回一个新查询 |

### 1.2 常用的SQLAlchemy查询执行器

| 方法           | 说明                                         |
| :------------- | :------------------------------------------- |
| all()          | 以列表形式返回查询的所有结果                 |
| first()        | 返回查询的第一个结果，如果未查到，返回None   |
| first_or_404() | 返回查询的第一个结果，如果未查到，返回404    |
| get()          | 返回指定主键对应的行，如不存在，返回None     |
| get_or_404()   | 返回指定主键对应的行，如不存在，返回404      |
| count()        | 返回查询结果的数量                           |
| paginate()     | 返回一个Paginate对象，它包含指定范围内的结果 |



先在python中直接创建好数据，创建数据的代码写在创建数据库的后面，代码如下:

```python
    ro1 = Role(name='admin')    db.session.add(ro1)    db.session.commit()    # 再次插入一条数据    ro2 = Role(name='user')    db.session.add(ro2)    db.session.commit()    us1 = User(name='wang', email='wang@163.com', password='123456', role_id=ro1.id)    us2 = User(name='zhang', email='zhang@189.com', password='201512', role_id=ro2.id)    us3 = User(name='chen', email='chen@126.com', password='987654', role_id=ro2.id)    us4 = User(name='zhou', email='zhou@163.com', password='456789', role_id=ro1.id)    us5 = User(name='tang', email='tang@itheima.com', password='158104', role_id=ro2.id)    us6 = User(name='wu', email='wu@gmail.com', password='5623514', role_id=ro2.id)    us7 = User(name='qian', email='qian@gmail.com', password='1543567', role_id=ro1.id)    us8 = User(name='liu', email='liu@itheima.com', password='867322', role_id=ro1.id)    us9 = User(name='li', email='li@163.com', password='4526342', role_id=ro2.id)    us10 = User(name='sun', email='sun@163.com', password='235523', role_id=ro2.id)    db.session.add_all([us1, us2, us3, us4, us5, us6, us7, us8, us9, us10])    db.session.commit()
```

重新运行程序，查看数据表中有没有新增数据:

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210525172150895.png"/>

正确运行后的结果如上图。

在上面的基础上进行查询如下：

进入pycharm内置的Python控制台:

```Python
from app import *User.query.all()		# 查询users表中有哪些数据User.query.count()		# 查询表中有多少条数据User.query.first()			# 查询表中的第一条数据User.query.get(4)			# 查询id为4的数据User.query.filter_by(id=4).first()			# 同上 注意写法User.query.filter(User.id==4).first()			# 同上 注意写法'''filter_by:属性=filter:对象.属性==filter功能更强大，可以实现更多的一些查询，支持比较运算符'''
```

**上述结果如下图:**

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210525175554685-1624169534725.png"/>



<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210525174147252.png"/>

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210525175615214.png"/>

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210525180057263.png"/>

## 十三、综合案例-图书管理-完结篇

代码:

```python
from flask import Flask,render_template,flash,request,url_for,redirect
from flask_sqlalchemy import SQLAlchemy
from flask_wtf import FlaskForm
from wtforms import StringField,SubmitField
from wtforms.validators import DataRequired

app = Flask(__name__)


#数据库配置：连接数据库/自动跟踪修改关闭
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:mysql@127.0.0.1/flask_books'
'''
务必将数据库创建好,记得指定数据库编码为UTF-8，即create database flask_books charset=utf8;
不然会报错
'''
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.secret_key='heima'      # 设置secret_key，不设置会报错

db = SQLAlchemy(app)        # 创建对象

'''
实例步骤描述:
1.配置数据库
    # 导入模块
    # 创建app实例并配置参数
    # mysql里创建好数据库
2.添加书和作者模型
    # 模型继承db.Model
    # __tablename__定义表名
    # db.Column定义字段
    # 关系引用
3.添加数据
4.使用模板显示数据库查询数据
 # 查询所有作者信息，让信息传递给模板
    # 模板中按照格式，依次for循环作者和书籍即可(作者获取书籍，用的是关系引用)
5.使用WTF使用表单
    # 自定义表单类
    # 模板中显示
    # secret_key 解决编码问题，csrf_token问题
6.实现相关的增删逻辑
    # 增加数据
    # 删除书籍  -- 网页中删除 -- 点击需要发送书籍的ID给删除书籍的路由 -- 路由需要接受参数
    
'''

# 作者模型
class Author(db.Model):     # 创建作者类
    __tablename__ = 'authors'       # 创建的表名
    id = db.Column(db.Integer,primary_key=True)     # 创建作者id字段
    name = db.Column(db.String(32),unique=True)     # 创建作者名称字段
    # 关系引用，即通过作者表中的作者id可以查询到与书表中作者id相同的数据
    # books是给自己（Author模型)用的，auther是给Book模型用的
    books = db.relationship('Book',backref='author')

    def __repr__(self):     # 返回结果格式化
        return 'Author: %s ' %self.name

# 书籍模型
class Book(db.Model):       # 创建书类
    # 表名
    __tablename__ = 'books'     # 创建的表名
    # 定义字段
    id = db.Column(db.Integer,primary_key=True)
    name = db.Column(db.String(32),unique=True)
    author_id = db.Column(db.Integer,db.ForeignKey('authors.id'))        # authors表的外键,表名.id

    def __repr__(self):     # 返回结果格式化
        return 'Book: %s %s ' %(self.name,self.author_id)

# 自定义表单类
class AuthorForm(FlaskForm):        # 创建表单类，用于在网页中显示表单时会用到
    author = StringField('作者',validators=[DataRequired()])      #创建作者输入框
    book = StringField('书籍',validators=[DataRequired()])        # 创建书名输入框
    submit = SubmitField('提交')      # 创建提交按钮


@app.route('/delete_author/<author_id>')        # 创建删除作者路由
def delete_author(author_id):
    # 查询数据库，是否有该ID的作者，如果有就删除，没有提示错误。
    author = Author.query.get(author_id)        # 查询传入的作者的id，若查询到即author有值，反之无值
    # 如果有就删除
    if author:      # 根据author判断，若数据库中存在这个作者
        try:
            Book.query.filter_by(author_id=author.id).delete()      # 根据作者id将书删除
            db.session.commit()     # 提交数据
        except Exception as e:
            print(e)        # 打印错误信息
            flash('删除作者出错')     # 在网页显示删除作者出错
            db.session.rollback()       # 数据库回滚，即撤销操作
    else:       # 若不存在
        # 没有提示错误
        flash('作者找不到')
    # return redirect('/')
    # redirect:重定向，需要传入域名/路由地址
    # url_for（’index‘）:需要传入视图函数名，返回视图函数对应的路由地址
    return redirect(url_for('index'))       # url_for('index')的返回结果为'/'即根目录，相当于redirect('/')重定向到根目录


@app.route('/delete_book/<book_id>')
def delete_book(book_id):
    # 查询数据库，是否有该ID的书，如果有就删除，没有提示错误。
    book = Book.query.get(book_id)
    # 如果有就删除
    if book:
        try:
            db.session.delete(book)
            db.session.commit()
        except Exception as e:
            print(e)
            flash('删除书籍出错')
            db.session.rollback()
    else:
        # 没有提示错误
        flash('书籍找不到')
    # return redirect('/')
    # redirect:重定向，需要传入域名/路由地址
    # url_for（’index‘）:需要传入视图函数名，返回视图函数对应的路由地址
    return redirect(url_for('index'))       # url_for('index')的返回结果为'/'即根目录，相当于redirect('/')重定向到根目录



@app.route('/',methods=['GET','POST'])
def index():
    # 创建自定义表单类
    author_form =AuthorForm()

    '''
    验证逻辑:
    1.调用WTF的验证函数实现验证
    2.验证通过获取数据
    3.判断作者是否存在
    4.如果作者存在，判断书籍是否存在，没有重复书籍就添加书籍，重复就提示错误
    5.如果作者不存在，直接添加作者和书籍
    6.验证不通过就提示错误    
    '''

    if author_form.validate_on_submit():
        # 验证通过获取数据
        author_name = author_form.author.data      #获取输入的作者数据
        book_name = author_form.book.data         # 获取输入的书名数据

        # 判断作者是否存在

        author = Author.query.filter_by(name = author_name).first()     # 查询输入的作者名称是否在数据库中存在
        if author:      # 进行判断语句
            book = Book.query.filter_by(name = book_name).first()
            if book:
                flash('已存在同名书籍')
            else:
                try:
                    new_book = Book(name=book_name,author_id=author.id)
                    db.session.add(new_book)
                    db.session.commit()
                except Exception as e:
                    print(e)
                    flash('添加书籍失败')
                    db.session.rollback()

        else:
            try:
                new_author = Author(name = author_name)
                db.session.add(new_author)
                db.session.commit()
                new_book = Book(name=book_name, author_id=new_author.id)
                db.session.add(new_book)
                db.session.commit()
            except Exception as e:
                print(e)
                flash('添加作者和书籍失败')
                db.session.rollback()
    else:
        # 验证不通过就提示错误
        if request.method == 'POST':
            flash('参数不全')


    # 查询所有的作者信息，让信息传递给模板
    authors = Author.query.all()

    '''
    验证逻辑:
    1.调用WTF的函数实现验证
    2.验证通过获取数据
    3.判断作者是否存在
    4.如果作者存在，判断书记是否存在，没有重复书籍就可以添加书籍，若重复，则提示错误
    5.如果作者不存在，添加作者和书籍。
    6.验证不通过就提示错误
    '''

    # 1.调用WTF的函数实现验证


    return render_template('books.html',authors=authors,form = author_form)

if __name__ == '__main__':
    db.drop_all()
    db.create_all()

    # 生成数据
    au1 = Author(name='老王')
    au2 = Author(name='老惠')
    au3 = Author(name='老刘')
    # 把数据提交给用户会话
    db.session.add_all([au1, au2, au3])
    # 提交会话
    db.session.commit()
    bk1 = Book(name='老王回忆录', author_id=au1.id)
    bk2 = Book(name='我读书少，你别骗我', author_id=au1.id)
    bk3 = Book(name='如何才能让自己更骚', author_id=au2.id)
    bk4 = Book(name='怎样征服美丽少女', author_id=au3.id)
    bk5 = Book(name='如何征服英俊少男', author_id=au3.id)
    # 把数据提交给用户会话
    db.session.add_all([bk1, bk2, bk3, bk4, bk5])
    # 提交会话
    db.session.commit()

    app.run(debug=True)
```



html:

```html
<!DOCTYPE html><html lang="en"><head>    <meta charset="UTF-8">    <title>Title</title></head><body><form method="post">    {{ form.csrf_token() }}    {{ form.author.label }}{{ form.author }}<br>    {{ form.book.label }}{{ form.book }}<br>    {{ form.submit}}<br>    {# 显示消息闪现内容 #}    {% for message in get_flashed_messages()%}        {{ message }}    {% endfor%}</form><hr><ul>    {% for author in authors %}        <li>{{ author.name }}<a href={{ url_for("delete_author",author_id=author.id) }}>删除</a></li>    <ul>        {% for book in author.books %}            <li>{{ book.name }}<a href={{ url_for("delete_book",book_id=book.id) }}>删除</a></li>            {% else %}                <li>无</li>        {% endfor%}    </ul>    {% endfor %}</ul></body></html>
```

运行结果：

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Flask%E5%85%A5%E9%97%A8/image-20210526203705733.png"/>

功能描述：

输入了作者和书籍，点击提交，会判断作者是否存在，存在就添加书籍，还会判断书是否存在，如果存在会提示书籍已存在，如果作者和书籍都不存在就都添加。点击删除可以实现删除，当作者没有书时会只显示一个无。

