---
title: Python面向对象OOP
top: true
cover: true
toc: true
mathjax: false
date: 2021-11-18 16:55:25
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/Python-OOP.jpg
coverImg:
password:
summary: Python-OOP
tags: Python
categories: Python
---

# Python面向对象OOP

> 面向对象的三大属性:
>
> 1. **封装** 根据 **职责** 将 **属性** 和 **方法** **封装** 到一个抽象的 **类** 中
> 2. **继承** **实现代码的重用**，相同的代码不需要重复的编写
> 3. **多态** 不同的对象调用相同的方法，产生不同的执行结果，**增加代码的灵活度**

## 1. 创建对象时自动调用初始化方法

- 当使用类名()创建对象时，为对象分配空间后，自动调用\_\_init__方法

```python
class Cat:
    def __init__(self):
        print('这是一个初始化方法！')

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat()
```

![image-20210528162622086](D:/1学习/1笔记/Linux基础_imgs/image-20210528162622086.png)

## 2.在初始化方法内部定义属性

```python
class Cat:
    def __init__(self):
        self.name = 'Tom'
        print('这是一个初始化方法！')

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat()
print(tom.name)
```

![image-20210528162751022](D:/1学习/1笔记/Linux基础_imgs/image-20210528162751022.png)

## 3.初始化同时设置初始值

```python
class Cat:
    def __init__(self,name):
        self.name = name
        print('这是一个初始化方法！')

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat('tom')
print(tom.name)
```

![image-20210528162908438](D:/1学习/1笔记/Linux基础_imgs/image-20210528162908438.png)

## 4.内置方法\_\_del__方法和对象生命周期

- 当一个对象被从内存中销毁前，会调用\_\_del__方法。
  - `__init__` 改造初始化方法，可以让创建对象更加灵活
  - `__del__` 如果希望在对象被销毁前，再做一些事情，可以考虑一下 `__del__` 方法

**生命周期**

* 一个对象从调用 `类名()` 创建，生命周期开始
* 一个对象的 `__del__` 方法一旦被调用，生命周期结束
* 在对象的生命周期内，可以访问对象属性，或者让对象调用方法

```python
class Cat:
    def __init__(self,name):
        self.name = name
        print('这是一个初始化方法！')

    def __del__(self):
        print('这个对象被销毁了')

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat('tom')
print(tom.name)
del tom		# del关键字可以删除一个对象
```

![image-20210528163536885](D:/1学习/1笔记/Linux基础_imgs/image-20210528163536885.png)

## 5.内置方法\_\_str__方法定制变量输入信息

```python
class Cat:
    def __init__(self,name):
        self.name = name
        print('这是一个初始化方法！')

    def __del__(self):
        print('这个对象被销毁了')

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat('tom')
print(tom.name)
print(tom)
del tom
```

当不自定义\_\_str__方法时，直接打印对象效果为:

![image-20210528163851294](D:/1学习/1笔记/Linux基础_imgs/image-20210528163851294.png)

可以看到打印出来的是**\_\_main__.类名 object at 对象的内存地址**

当我们自定义了之后：

```python
class Cat:
    def __init__(self,name):
        self.name = name
        print('这是一个初始化方法！')

    def __del__(self):
        print('这个对象被销毁了')

    def __str__(self):
        return '我最帅'

# 使用类名()创建对象的时候，会自动调用初始化方法(__init__)
tom = Cat('tom')
print(tom.name)
print(tom)
del tom
```

![image-20210528164052790](D:/1学习/1笔记/Linux基础_imgs/image-20210528164052790.png)打印出了我们设置的返回的内容。



## 6.封装特性和案例

### 1.封装的概念

1. **封装** 是面向对象编程的一大特点
2. 面向对象编程的 **第一步** —— 将 **属性** 和 **方法** **封装** 到一个抽象的 **类** 中
3. **外界** 使用 **类** 创建 **对象**，然后 **让对象调用方法**
4. **对象方法的细节** 都被 **封装** 在 **类的内部**

### 2.小明爱跑步案例

```python
class Person:

    def __init__(self,name,weight):
        self.name = name
        self.weight = weight

    def __str__(self):
        return f'我的名族叫:{self.name},我的体重是:{self.weight}公斤'

    def run(self):
        print(f'{self.name}爱跑步')
        self.weight -= 0.5

    def eat(self):
        print(f'{self.name}爱跑步')
        self.weight += 1

xiaoming = Person('小明',75.0)
print(xiaoming)
xiaoming.run()
print(xiaoming)
xiaoming.eat()
print(xiaoming)
```

![image-20210528165213151](D:/1学习/1笔记/Linux基础_imgs/image-20210528165213151.png)

### 3.多个对象之间互不干扰

```python
class Person:

    def __init__(self,name,weight):
        self.name = name
        self.weight = weight

    def __str__(self):
        return f'我的名族叫:{self.name},我的体重是:{self.weight}公斤'

    def run(self):
        print(f'{self.name}爱跑步')
        self.weight -= 0.5

    def eat(self):
        print(f'{self.name}爱跑步')
        self.weight += 1

xiaoming = Person('小明',75.0)
xiaomei = Person('小美',45.0)
print(xiaoming)
xiaoming.run()
print(xiaoming)
xiaoming.eat()
print(xiaoming)

print('='*50)

print(xiaomei)
xiaomei.eat()
print(xiaomei)
xiaomei.run()
print(xiaomei)
```

![image-20210528165547278](D:/1学习/1笔记/Linux基础_imgs/image-20210528165547278.png)

### 3.实例2-拜访家具

```python
class HouseItem:

    def __init__(self,name,area):
        self.name = name
        self.area = area

    def __str__(self):
        return f'{self.name},占地面积是{self.area}平方'

class House:

    def __init__(self,house_type,area):
        self.house_type = house_type
        self.area = area
        self.free_area = area
        self.item_list = []

    def __str__(self):
        return f'房子户型是{self.house_type},占地面积是{self.area}'

    def add_item(self,item):
        if self.area >= item.area:
            self.item_list.append(item.name)
            self.free_area -= item.area
        else:
            print('房子空间不足！')


bed = HouseItem('席梦思',4.0)
chest = HouseItem('衣柜',2.0)
table = HouseItem('餐桌',1.5)

print(bed)
print(chest)
print(table)

house = House('三室一厅',50)
print(house)
house.add_item(bed)
house.add_item(chest)
house.add_item(table)
print(house.item_list)
print(house.free_area)
```

![image-20210528171038553](D:/1学习/1笔记/Linux基础_imgs/image-20210528171038553.png)

### 4.士兵突击

```python
class Gun:

    def __init__(self,model):
        self.model = model
        self.bullet_count = 0

    def add_bullet(self,count):
        self.bullet_count += count

    def shoot(self):
        if self.bullet_count == 0:
            print(f'{self.model}子弹不足！')
            return
        print('biubiubiu')
        self.bullet_count -= 1


class Soldier:

    def __init__(self,name):
        self.name = name
        self.gun = None

    def fire(self):
        if self.gun is None:
            print(f'{self.name}还没有枪！')
            return
        print(f'冲啊{self.name}...')
        self.gun.add_bullet(50)
        self.gun.shoot()


ak47 = Gun('ak47')

xushanduo = Soldier('许三多')
xushanduo.fire()
xushanduo.gun = ak47
print(xushanduo.gun)
xushanduo.fire()
```

![image-20210528173105378](D:/1学习/1笔记/Linux基础_imgs/image-20210528173105378.png)

## 7.私有属性和私有方法

### 1.私有属性

```python
class Women:
    def __init__(self,name):
        self.name = name
        self.__age = 18

    def secret(self):
        print(f'我的名字是{self.name}，年龄是{self.__age}')

xiaomei = Women('小美')
xiaomei.secret()
print(xiaomei.__age)
```

![image-20210528174122833](D:/1学习/1笔记/Linux基础_imgs/image-20210528174122833.png)

- 程序运行后发现报了一个错误， 'Women' object has no attribute '__age'，说明age属性不能直接被访问，而可以通过类中方法访问。

### 2.私有方法

```python
class Women:
    def __init__(self,name):
        self.name = name
        self.__age = 18

    def __secret(self):
        print(f'我的名字是{self.name}，年龄是{self.__age}')

xiaomei = Women('小美')
xiaomei.secret()
```

- 上面代码中，我将之前的secret方法名的前面加上了两个下划线，这个方法就变成了私有方法，只有在类中可以调用，而想在类的外面调用就会报错:

![image-20210528174520744](D:/1学习/1笔记/Linux基础_imgs/image-20210528174520744.png)

### 3.伪私有属性和伪私有方法

```python
class Women:
    def __init__(self,name):
        self.name = name
        self.__age = 18

    def __secret(self):
        print(f'我的名字是{self.name}，年龄是{self.__age}')

xiaomei = Women('小美')
xiaomei._Women__secret()
print(xiaomei._Women__age)
```

![image-20210528174708148](D:/1学习/1笔记/Linux基础_imgs/image-20210528174708148.png)

- 当定义一个私有属性时，如__age，python会将它转换为\_Women\_\_age，所有我们可以使用xiaomei._Women__age来访问私有属性。同理，私有方法也是一样。

### 8.继承

### 1.单继承

```python
class Animal:

    def eat(self):
        print('吃')

    def drink(self):
        print('喝')

    def run(self):
        print('跑')

    def sleep(self):
        print('睡')

class Dog(Animal):

    def bark(self):
        print('汪汪叫')

wangcai = Dog()
wangcai.eat()
wangcai.drink()
wangcai.run()
wangcai.sleep()
wangcai.bark()
```

- 上面的代码中，我们并没有在Dog类中定义eat、drink、run、sleep，但却可以调用，这是因为Dog类继承了Animal的方法。

![image-20210528175658518](D:/1学习/1笔记/Linux基础_imgs/image-20210528175658518.png)

### 3.继承的传递性

```python
class Animal:

    def eat(self):
        print('吃')

    def drink(self):
        print('喝')

    def run(self):
        print('跑')

    def sleep(self):
        print('睡')

class Dog(Animal):

    def bark(self):
        print('汪汪叫')

class XiaoTianQuan(Dog):
    def fly(self):
        print('我会飞')

wangcai = XiaoTianQuan()
wangcai.eat()
wangcai.drink()
wangcai.run()
wangcai.sleep()
wangcai.bark()
wangcai.fly()
```

- 上面的程序中Dog类继承了Animal类，XiaoTianQuan类继承了Dog类，这样XiaoTianQuan类就拥有了Animal类和Dog类的所有属性和方法。

![image-20210528180244751](D:/1学习/1笔记/Linux基础_imgs/image-20210528180244751.png)

### 4.方法的重写

```python
class Animal:

    def eat(self):
        print('吃')

    def drink(self):
        print('喝')

    def run(self):
        print('跑')

    def sleep(self):
        print('睡')

class Dog(Animal):

    def bark(self):
        print('汪汪叫')

class XiaoTianQuan(Dog):
    def fly(self):
        print('我会飞')
    def bark(self):
        print('叫得跟普通狗不一样')
xtq = XiaoTianQuan()

xtq.bark()
```

- 虽然父类中已经定义了bark方法，但是在XiaoTianQuan类中又重新定义了一个bark方法，当对象调用法法时，会调用自身类的方法。

![image-20210528191518111](D:/1学习/1笔记/Linux基础_imgs/image-20210528191518111.png)

### 5.扩展父类方法，super()对象调用父类方法

```python
class Animal:

    def eat(self):
        print('吃')

    def drink(self):
        print('喝')

    def run(self):
        print('跑')

    def sleep(self):
        print('睡')

class Dog(Animal):

    def bark(self):
        print('汪汪叫')

class XiaoTianQuan(Dog):
    def fly(self):
        print('我会飞')
    def bark(self):
        print('叫得跟普通狗不一样')
        super().bark()
xtq = XiaoTianQuan()

xtq.bark()
```

- super().bark()调用父类的方法

![image-20210528191952131](D:/1学习/1笔记/Linux基础_imgs/image-20210528191952131.png)

### 6.使用父类名调用父类方法

```python
class Animal:

    def eat(self):
        print('吃')

    def drink(self):
        print('喝')

    def run(self):
        print('跑')

    def sleep(self):
        print('睡')

class Dog(Animal):

    def bark(self):
        print('汪汪叫')

class XiaoTianQuan(Dog):
    def fly(self):
        print('我会飞')
    def bark(self):
        print('叫得跟普通狗不一样')
        Dog.bark(self)

xtq = XiaoTianQuan()

xtq.bark()
```

- Dog.bark(self)即使用父类名调用父类方法

![image-20210528192745016](D:/1学习/1笔记/Linux基础_imgs/image-20210528192745016.png)

## 8.父类的私有属性和方法

### 1.父类的私有属性和方法

- 在子类中**不能**直接调用父类的**私有属性和私有方法**

```python
class A:

    def __init__(self):
        self.num1 = 100
        self.__num2 = 200
    def __test(self):
        print(f'这是A类的私有方法，{self.num1},{self.__num2}')

class B(A):
    def demo(self):
        print(self.__num2,self.__test())

b = B()
b.demo()
```

![image-20210528193738902](D:/1学习/1笔记/Linux基础_imgs/image-20210528193738902.png)

### 2.通过父类的共有方法间接访问父类的私有方法和属性

```python
class A:

    def __init__(self):
        self.num1 = 100
        self.__num2 = 200
    def __test(self):
        print(f'这是A类的私有方法，{self.num1},{self.__num2}')

    def test(self):
        print(f'私有方法:{self.__num2}')
        self.__test()

class B(A):
    def demo(self):
        print(f'共有属性:{self.num1}')
        self.test()

b = B()
b.demo()
```

- 可以通过父类的共有方法访问父类属性和调用父类方法

![image-20210528194216014](D:/1学习/1笔记/Linux基础_imgs/image-20210528194216014.png)

## 9.多继承

### 1.多继承

```python
class A:
    def test(self):
        print('test方法')

class B:
    def demo(self):
        print('demo方法')

class C(A,B):
    pass

c = C()
c.test()
c.demo()
```

- 多继承使子类继承所有父类的所有属性和方法。

![image-20210528194523287](D:/1学习/1笔记/Linux基础_imgs/image-20210528194523287.png)

- 若继承的多个类中的方法有重名的情况，会调用存在同名的继承的类的第一个。

### 2.MRO方法搜索顺序

```python
class A:
    def test(self):
        print('A----test方法')

    def demo(self):
        print('A----demo方法')

class B:
    def test(self):
        print('B----test方法')

    def demo(self):
        print('B----demo方法')

class C(A,B):       # 继承A,B类
    pass

c = C()
c.test()
c.demo()
print(C.__mro__)
```

print(C.__mro__)打印一个类的MRO

![image-20210528195505628](D:/1学习/1笔记/Linux基础_imgs/image-20210528195505628.png)

- 输出了一个元组，这个元组代表当对象执行一个属性或者方法时，调用的顺序，先是在自己类中查找，找不到再去第一个父类，接着第二个。

### 3.super()函数:调用父类的构造方法

>使用super()函数，但如果涉及多继承，该函数只能调用第一个直接父类的构造方法。
>
>Super().\_\_init__会调用第一个父类的构造方法。
>
>那如果要调用多个父类的构造方法该如何实现呢？只需要父类名.\_\_init__(self)即可实现



### 4.新式类和经典类

> `object` 是 `Python` 为所有对象提供的 **基类**，提供有一些内置的属性和方法，可以使用 `dir` 函数查看

* **新式类**：以 `object` 为基类的类，**推荐使用**
* **经典类**：不以 `object` 为基类的类，**不推荐使用**

* 在 `Python 3.x` 中定义类时，如果没有指定父类，会 **默认使用** `object` 作为该类的 **基类** —— `Python 3.x` 中定义的类都是 **新式类**
* 在 `Python 2.x` 中定义类时，如果没有指定父类，则不会以 `object` 作为 **基类**

> **新式类** 和 **经典类** 在多继承时 —— **会影响到方法的搜索顺序**

```python
class A(object):
    pass

a = A()
dir(a)
```

```python
['__class__',
 '__delattr__',
 '__dict__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__module__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '__weakref__']
```

上面这些都是基类object自带的方法。



## 10.多态

### 1.多态的概念

- **多态***：不同的子类对象条用相同的父类方法，产生不同的执行结果

  - **多态**可以增加代码的灵活度
  - 以**继承**和**重写父类方法**为前提
  - 是调用方法的技巧，**不会影响到类的内部设计**


### 2.实例

  ```python
class Dog:

    def __init__(self,name):
        self.name = name

    def game(self):
        print(f'{self.name}蹦蹦跳跳的玩耍！')

class XiaoTianQuan(Dog):

    def game(self):
        print(f'{self.name}飞到天上去玩耍！')

class Person:
    def __init__(self,name):
        self.name = name

    def geme_with_dog(self,dog):
        print(f'{self.name}和{dog.name}快乐的玩耍！')
        dog.game()

wangcai = Dog('旺财')
wangcai1 = XiaoTianQuan('飞天旺财')
xiaoming = Person('小明')
xiaoming.geme_with_dog(wangcai)
print('='*50)
xiaoming.geme_with_dog(wangcai1)
  ```

- 可以看到针对传入不同的对象输出的结果是不一样的。

![image-20210528210551765](D:/1学习/1笔记/Linux基础_imgs/image-20210528210551765.png)



## 11.类属性

### 1.类属性的概念

> Python中万物皆对象，类也是一个对象，class AAA()定义的称为类对象
>
> 用类创建的对象叫做实例对象。

- 类属性就是给类对象中定义的属性
- 通常用来记录与这个类相关的特性
- 类属性不会用于记录具体对象的特此

```python
class Tool:

    # 定义类属性
    count = 0

    def __init__(self,name):
        self.name = name
        Tool.count += 1


tool1 = Tool('斧头')
tool2 = Tool('榔头')
tool3 = Tool('水桶')
print(Tool.count)
```

![image-20210528220426169](D:/1学习/1笔记/Linux基础_imgs/image-20210528220426169.png)



### 2.类属性的查找机制

> 访问类属性可以通过 **类名.类属性** 的方，在一定的情况下也可以通过 **对象名.类属性**，程序是如何做到的呢？
>
> 当实例对象访问某个属性时，会先查找是否有这个实例属性，如果找不到就会查找类属性是否有这个属性。

```python
class Tool:

    # 定义类属性
    count = 0

    def __init__(self,name):
        self.name = name
        Tool.count += 1


tool1 = Tool('斧头')
tool2 = Tool('榔头')
tool3 = Tool('水桶')
print(Tool.count)
print(tool1.count)
```

![image-20210528221045134](D:/1学习/1笔记/Linux基础_imgs/image-20210528221045134.png)

运行结果表示: **属性名.类属性** 在一定的情况下是可以实现的。



## 12.类方法

> - 类方法就是针对类对象定义的方法
>
> - 在类方法内部可以直接访问类属性或者调用其他的类方法
> - 类方法需要用装饰器修饰`@classmethod`来标识，告诉解释器这是一个类方法
> - 类方法的第一个参数是cls
>   - 由哪一个类调用的方法，方法内的`cls`就是哪一个类的引用
>   - 这个参数和实例方法的第一个参数是self类似
> - 通过**类名.类方法名**调用，调用方法时，不需要传递cls参数
> - 在方法内部
>   - 可以通过cls.访问类的属性
>   - 也可以通过cls.调用其他的类方法

- 语法：

```python
@classmethod
def 类方法名(cls):
    pass
```

- 实例：

```python
class Tool:

    # 定义类属性
    count = 0

    def __init__(self,name):
        self.name = name
        Tool.count += 1

    @classmethod
    def show_tool_count(cls):
        print('工具对象的数量:',cls.count)

tool1 = Tool('斧头')
tool2 = Tool('榔头')
tool3 = Tool('水桶')

Tool.show_tool_count()
```

![image-20210528232047060](D:/1学习/1笔记/Linux基础_imgs/image-20210528232047060.png)

## 13.静态方法

> - 静态方法
>   - 既不需要访问实例属性或者调用实例方法
>   - 也不需要访问类属性或者调用类方法

- 语法：

```python
@staticmethod
def 静态方法名():
    pass
```

- 实例：

```python
class Tool:

    # 定义类属性
    count = 0

    def __init__(self,name):
        self.name = name
        Tool.count += 1

    @classmethod
    def show_tool_count(cls):
        print('工具对象的数量:',cls.count)

    @staticmethod
    def static_method():
        print('这是一个静态方法')

tool1 = Tool('斧头')
tool2 = Tool('榔头')
tool3 = Tool('水桶')

Tool.show_tool_count()
tool1.static_method()
Tool.static_method()
```

- 静态方法可以不用创建对象就可以调用，即用类名直接访问。

![image-20210528232511763](D:/1学习/1笔记/Linux基础_imgs/image-20210528232511763.png)



## 14.方法综合-案例分析

```python
class Game:
    top_score = 0		# 创建类属性
    def __init__(self,player_name):		# 构造函数
        self.player_name = player_name

    @staticmethod		# 创建静态方法
    def show_help():
        print('帮助信息:让僵尸进入大门！')

    @classmethod
    def show_top_score(cls):		# 创建类方法
        print('历史最高分为:',cls.top_score)

    def start_game(self):		# 创建实例方法
        print(f'{self.player_name}准备好，要开始游戏咯')


Game.show_help()		# 通过类名调用静态方法
Game.show_top_score()		# 调用类方法
user1 = Game('葫芦娃')		# 创建实例对象
user1.start_game()		# 调用实例方法
```

![image-20210528233538393](D:/1学习/1笔记/Linux基础_imgs/image-20210528233538393.png)



## 15.\_\_new__方法

> - 使用类名()创建对象时，Python解释器首先会调用\_\_new__方法为对象分配空间。
> - \_\_new__是一个有object基类提供的内置的静态方法。
>   - 在内存中为对象分配空间
>   - 返回对象的引用
> - Python的解释器获得对象的引用后，将引用作为第一个参数，传递给\_\_init__方法。



> 重写\_\_new__方法的代码非常固定。

- 重写\_\_new\_\_方法一定要 return super().\_\_new__(cls)
- 否则Python的解释器得不到分配空间的对象引用，就不会调用初始化方法。
- 注意:\_\_new__是一个静态方法，在调用时需要主动传递cls参数

```python
class MusicPlayer:
    def __new__(cls, *args, **kwargs):
        print('这是new方法')
        return super().__new__(cls)


    def __init__(self):
        print('这是初始化方法！')

mp3 = MusicPlayer()
print(mp3)
```

![image-20210529111034327](D:/1学习/1笔记/Linux基础_imgs/image-20210529111034327.png)

new方法重写格式如下：

```python
class Person(object):
    def __new__(cls):
        return  object.__new__(cls)
```

- __new__至少要有一个参数cls，代表要实例化的类，此参数在实例化时由Python解释器自动提供；**__new__必须要有返回值，返回实例化出来的实例，可以return父类new出来的实例，或直接是object的new出来的实例。**

- object.**new**(cls)执行完返回的结果为Person类的实例对象

```python
class Person(object):
    def __init__(self):
        print("__init__")
        self.name="张三"
    def __new__(cls):
        print('__new__')
        ob = object.__new__(cls)#ob为Person实例对象
        print(ob)
        return ob
p1 = Person()
print(p1.name)
```

![image-20210529111609191](D:/1学习/1笔记/Linux基础_imgs/image-20210529111609191.png)

- p1=Person()该语句主要做了以下工作：
  **首先调用Person的__new__方法，该方法通过object.\_\_new\_\_(cls)创建了Person实例对象，并返回。最后调用了该Person实例对象的\_\_init\_\_方法。**



- object.**new**()方法接收的参数是类对象，可以不是当前类对象cls，如果将cls换成其他类对象会发生什么呢，看下面代码的运行结果：

```python
class Dog(object):
    def __init__(self):
        self.name="旺财"
        print("Dog.__init__")
class Person(object):
    def __init__(self):
        self.name="张三"
        print("Person.__init__")
    def __new__(cls):
        print('__new__')
        ob = object.__new__(Dog)
        return ob
p1 = Person()
print(type(p1))
```

![image-20210529114107821](D:/1学习/1笔记/Linux基础_imgs/image-20210529114107821.png)

- 由结果得知p1是Dog类的实例，但是有个问题，Python解释器没有自动执行__init__方法，由结果可以看出并没有打印字符串__init__。**若__new__()没有正确返回当前类cls的实例，那__init__()将不会被调用。**



## 16.单例设计模式

> 单例 - - 让类创建的对象，在系统中只有唯一一个实例
>
> 1. 定义一个类属性，初始值是None，用于记录单例对象的引用
> 2. 重写new方法
> 3. 如果类属性is none ，调用父类方法分配空间，并在类属性中记录结果
> 4. 返回类属性中记录的对象引用

```python
class MusicPlayer:
    instance = None
    def __new__(cls, *args, **kwargs):
        if cls.instance is None:
            cls.instance = super().__new__(cls)
        return cls.instance

    def __init__(self,name):
        self.name = name

m1 = MusicPlayer('m1')
print(m1)
print(m1.name)
m2 = MusicPlayer('m2')
print(m2)
print(m2.name)
```

![image-20210529115728934](D:/1学习/1笔记/Linux基础_imgs/image-20210529115728934.png)

- 根据运行结果可以得出，对象的内存地址都是一样的，并没有分配多余空间。
- 但是初始化方法执行了多次。



> 若想让初始化方法只执行一次：

```python
class MusicPlayer:
    instance = None
    init_flag = False
    def __new__(cls, *args, **kwargs):
        if cls.instance is None:
            cls.instance = super().__new__(cls)
        return cls.instance

    def __init__(self,name):
        if not MusicPlayer.init_flag:
            print('初始化播放器')
            MusicPlayer.init_flag = True

m1 = MusicPlayer('m1')
print(m1)
m2 = MusicPlayer('m2')
print(m2)
```

![image-20210529120137952](D:/1学习/1笔记/Linux基础_imgs/image-20210529120137952.png)

- 只需在类中再创建一个类属性，在初始化方法中根据这个类属性的值判断是否执行。
