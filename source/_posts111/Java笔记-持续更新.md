---
title: Java一些内置方法-持续更新
top: false
cover: false
toc: true
mathjax: false
date: 2021-04-27 12:40:28
author:
img: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Java%E5%B0%81%E9%9D%A2/Java.jpg
coverImg: https://cdn.jsdelivr.net/gh/zhaotaogit/images/Java%E5%B0%81%E9%9D%A2/Java.jpg
password:
summary: Java学习
tags:
	Java
categories: Java
---



# Java 笔记

### 1. [Java split()用法方法](https://www.cnblogs.com/xiaoxiaohui2015/p/5838674.html)

- 例：

  ``` java
  import java.util.Arrays;
  
  String address="上海\\上海市|闵行区\\吴中路";
  String[] splitAddress=address.split("\\\\");
  System.out.println(Arrays.toString(splitAddress));
  ```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Java%E4%B8%80%E4%BA%9B%E5%86%85%E7%BD%AE%E6%96%B9%E6%B3%95/image-20210531174727105.png"/>

> 实现按字符切分

split:特殊符号不适应：. | \ $ +，如果要用，需要加转义符或者：

```java
String str = "hello.world";
StringTokenizer token = new StringTokenizer(str,".");
// 判断有没有下一个元素，有就是true
while (token.hasMoreElements()) {
    // 取出当前元素
    System.out.println(token.nextToken());
}
```



### 2.Java substring()方法

  ```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
String s = sc.nextLine();
System.out.println(s.substring(0, 2));  //提取下标为0-2(不包括2)的下标
System.out.println(s.substring(s.length()-1));  //提取最后一个字符
  ```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Java%E4%B8%80%E4%BA%9B%E5%86%85%E7%BD%AE%E6%96%B9%E6%B3%95/image-20210531174818062.png"/>

> 实现根据下标取字符

### 3.Arrays.toString()方法

```java
import java.util.Arrays;

String string[] = {"abc","def","igh"};
System.out.println(Arrays.toString(string));
```

<img src="https://cdn.jsdelivr.net/gh/zhaotaogit/images/Java%E4%B8%80%E4%BA%9B%E5%86%85%E7%BD%AE%E6%96%B9%E6%B3%95/image-20210531172051448.png"/>

> 如果想要把数组中的内容打印出来,直接调用toString()方法只会打印出数组的地址,因此需要使用Arrays的toString()方法。这个方法是是用来将数组转换成String类型输出的，入参可以是long，float，double，int，boolean，byte，object型的数组。

### 3.运算符`==`和 `String` 类的 `equals` 方法

- 使用“==”比较两个字符串，是比较两个对象在内存中的地址是否一致，本质上就是判断两个变量是否指向同一个对象，如果是则返回 true，否则返回 false。
- 而 `String` 类的 `equals` 方法则是比较两个 `String` 字符串的内容是否一致，返回值也是一个布尔类型。

```java
public static void main(String[] args) {
        String a = "a";
        String b = new String("a");
        System.out.println(a);
        System.out.println(b);
        System.out.println(a == b); // 返回false，new一定会开辟新内存空间
        System.out.println(a.equals(b));
    }
```

![image-20211120142953407](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120142953407.png)

### 4.String类的常用方法

- `public char charAt(int index)`

  返回 index 指定的索引处的字符。

- `public int length()`

  返回此字符串的长度。这里需要和获取数组长度区别开，获取数组长度是通过`数组名.length`获取的。

- `public int indexOf(String str)`

  返回指定子字符串 str 在此字符串中第一次出现处的索引。

- `public int indexOf(String str,int fromIndex)`

  返回指定子字符串 str 在此字符串中第一次出现处的索引，从指定的索引 fromIndex 处开始搜索。

- `public boolean equalsIgnoreCase(String another)`

  将此 String 与另一个字符串 another 比较，比较时不区分大小写。

- `public String replace(char oldChar,char newChar)`

  返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。

```java
public static void main(String[] args) {
        String s1 = "blue bridge";
        String s2 = "Blue Bridge";
        System.out.println(s1.charAt(1));
        System.out.println(s1.length());
        System.out.println(s1.indexOf("bridge"));
        System.out.println(s1.indexOf("Bridge"));
        System.out.println(s1.equalsIgnoreCase(s2));

        String s = "我是学生，我在学Java!";
        String str = s.replace("我","你");
        System.out.println(str);
    }
```

![image-20211120144419520](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120144419520.png)

- `public boolean startsWith(String prefix)`

  判断此字符串是否以 prefix 指定的前缀开始。

- `public boolean endsWith(String suffix)`

  判断此字符串是否以 suffix 指定的后缀结束。

- `public String toUpperCase()`

  将此 String 中的所有字符都转换为大写。

- `public String toLowerCase()`

  将此 String 中的所有字符都转换为小写。

- `public String substring(int beginIndex)`

  返回一个从 beginIndex 开始到结尾的新的子字符串。

- `public String substring(int beginIndex,int endIndex)`

  返回一个从 beginIndex 开始到 endIndex 结尾（不含 endIndex 所指字符）的新的子字符串。

- `public String trim()`

  返回字符串的副本，忽略原字符串前后的空格。

```java
public static void main(String[] args) {
        String fileName = "20200801柳海龙Resume.docx";
        System.out.println(fileName.startsWith("2014"));
        System.out.println(fileName.endsWith("docx"));
        System.out.println(fileName.endsWith("doc"));
        System.out.println(fileName.toLowerCase());
        System.out.println(fileName.toUpperCase());
        System.out.println(fileName.substring(8));
        System.out.println(fileName.substring(8,11));
        String fileName2 = "  20200801柳海龙Resume  .docx";
        System.out.println(fileName2.trim());
    }
```

![image-20211120145058922](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120145058922.png)

- `public static String valueOf(基本数据类型参数)`

  返回基本数据类型参数的字符串表示形式，例如：

  ```java
  public static String valueOf(int i)
  public static String valueOf(double d)
  ```

  这两个方法是 String 类的静态方法，关于“静态”的内容将会在后面的课程详细介绍，这里需要大家注意的是，静态方法是通过**类名.方法名**直接调用的，例如：

  ```java
  String result = String.valueOf(100);//将int型100转换为字符串"100"
  ```

- `public String[] split(String regex)`

  通过 regex 指定的分隔符分隔字符串，返回分隔后的字符串数组。

```java
public static void main(String[] args) {
        String result = String.valueOf(100);
        Scanner input = new Scanner(System.in);
        System.out.print("请输入您去年一年的薪水总和:");
        int lastSalary = input.nextInt();
        String strSalary = String.valueOf(lastSalary);
        System.out.println("您去去年一年的薪水总和是：" + strSalary.length() + "位数！");
        String date = "Mary,F,1976";
        String[] splitStr = date.split(",");
        System.out.println("Mary,F,1976使用，分隔后的结果是：");
        for (int i = 0;i<splitStr.length;i++) {
            System.out.println(splitStr[i]);
        }
    }
```

![image-20211120152703647](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120152703647.png)

### 5.StringBuffer的用法

> 字符串的值在创建之后不能更改。我们平时“改变”字符串值的方式，其实是先产生新的字符串，然后将原引用指向新的字符串，这样看起来就像改变了字符串一样。显然，如果需要频繁修改字符串的值，使用 String 就显得低效了。是否存在一个类，既可以存储字符串，又能对这个字符串自身进行修改而尽量少地产生新字符串呢？可以，这个类就是 `StringBuffer`。StringBuffer 字符串代表的是可变的字符序列，可以对字符串对象的内容进行修改。

以下是 StringBuffer 类最常用的构造方法。

- `StringBuffer()`：构造一个空白的字符串缓冲区，其初始容量为 16 个字符。
- `StringBuffer(String str)`：构造一个字符串缓冲区，并将其内容初始化为指定的字符串内容。

以下是通过 `StringBuffer` 类的构造方法创建 StringBuffer 字符串的代码。

```java
StringBuffer strB1 = new StringBuffer();
System.out.println(strB1.length());
```

以上通过 `strB1.length()`返回的字符串长度是 0。但实际上，strB1 的底层创建了一个长度为 16 的字符数组，为接收字符串内容做准备。

```java
StringBuffer strB2 = new StringBuffer("柳海龙");
System.out.println(strB2.length());
```

通过`strB2.length()`返回长度是 3，实际在底层创建了一个长度为 3+16 的字符数组。

StringBuffer 上的主要操作是 `append` 和 `insert` 方法，将字符追加或插入到字符串缓冲区中。`append` 方法始终将字符添加到缓冲区的末端，而 `insert` 方法则在指定的位置添加字符。

以下是 `StringBuffer` 类的常用方法。

- `public StringBuffer append(String str)`

  将 str 指定的字符串追加到此字符序列的末尾。

- `public StringBuffer append(StringBuffer str)`

  将 str 指定的 StringBuffer 字符串追加到此序列的末尾。

- `public StringBuffer append(char[] str)`

  将 str 指定的字符数组追加到此序列的末尾。

- `public StringBuffer append(char[] str,int offset,int len)` 自索引 offset 开始截取 str 的 len 个字符追加到此序列中。

- `public StringBuffer append(double d)`

  将 double 类型的变量 d 的字符串表示形式追加到此序列的末尾。

- `public StringBuffer append(Object obj)`

  将参数 obj 的字符串表示形式追加到此序列的末尾。

- `public StringBuffer insert(int offset,String str)`

  将字符串 str 插入到此字符序列中，offset 表示插入位置。

```java
public static void main(String[] args) {
        System.out.println("创建StringBuffer对象");
        StringBuffer strB1 = new StringBuffer();
        System.out.println("new StringBuffer()创建对象的长度为:" + strB1.length());
        StringBuffer strB2 = new StringBuffer("柳海龙");
        System.out.println("new StringBuffer(\"柳海龙\"创建对象的长度为:" + strB2.length());
        System.out.println("strB2例的内容为：" + strB2);
        System.out.println("使用append方法追加字符串");
        strB2.append(",您好");
        System.out.println(strB2);
        strB2.insert(3,"工程师");
        System.out.println(strB2);
    }
```

![image-20211120153652422](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120153652422.png)

除了 StringBuffer 以外，还存在另一个可变的字符串类 StringBuilder。StringBuilder 类是在 Java 5.0 中被提出的，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法是非线程安全的，而 StringBuffer 是线程安全的。

**内存模型**

StringBuffer 是一个内容可变的字符序列，或者说它是一个内容可变的字符串类型。当使用 `StringBuffer strB1 = new StringBuffer("柳海龙");`语句创建 StringBuffer 对象时，内存结构示意图如图所示。

![](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/20211120160921.png)

当使用`strB1.append("工程师")`方法时，将之前创建的 StringBuffer 对象的内容“柳海龙”修改成“柳海龙工程师”，内存结构示意图如图所示。

![](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/20211120161011.png)

### 6.日期类

> Java 中有两套常用的日期类，一套是从 JDK1.0 开始并经过了多次升级的日期类，一套是从 JDK8.0 开始提供的新日期类。

#### JDK8.0 以前的 Date 类

用于定义当前的日期和时间。例如，在下面的程序中创建了一个 Date 对象，它就表示当前的时间。

```java
import java.util.Date;
public class TestDate1{
    public static void main(String[] args) {
        Date date = new Date();
        System.out.println(date);
    }
}
```

运行结果如图所示。

![图片描述](https://doc.shiyanlou.com/courses/3232/1533757/0b2ad7af8bb7b4a33447702779459b22-0)

以下是 Date 定义的常用方法。

- `Date(long millisec)`

  带一个参数的 Date 构造方法，该参数是从 1970 年 1 月 1 日零点起的毫秒数。

- `long getTime()`

  返回自 1970 年 1 月 1 日 零点以来，此 Date 对象经过的毫秒数。

- `boolean after(Date date)`

  判断当前对象是否在参数 date 指定的日期之后。如果是返回 true,否则返回 false。

- `boolean before(Date date)`

  判断当前对象是否在参数 date 指定的日期之前。如果是返回 true,否则返回 false。

```java
public static void main(String[] args) {
        Date date1 = new Date(10000000);
        Date date2 = new Date();
        boolean isBefore = date1.before(date2);
        boolean isAfter = date1.after(date2);

        System.out.println(isBefore);
        System.out.println(isAfter);
    }
```

![image-20211120164148228](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120164148228.png)

#### JDK8.0 提供的 Date 类

在 JDK8.0 提供的新日期 API 中，所有的类都是不可变的，这就对高并发编程提供了友好支持。并且新的 API 将“时间”的概念更加精细化，提供了日期（Date）、时间（Time）、日期时间（DateTime）、时间戳（unix timestamp）以及时区等细化的时间类。

JDK8.0 新增的日期 API 都在 `java.time` 包下，其中常见的 API 如下表所示。

| API           | 含义                             |
| ------------- | -------------------------------- |
| Instant       | 时间戳                           |
| LocalDate     | 日期，如 2020-06-16              |
| LocalTime     | 时刻，如 11:52:52                |
| LocalDateTime | 具体时间，如 2020-06-16 11:52:52 |

```java
import java.time.*;

public class TestNewDate1 {
    public static void main(String[] args) {
        Instant instant = Instant.now();
        LocalDate localDate = LocalDate.now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();
        ZonedDateTime zonedDateTime = ZonedDateTime.now();
        System.out.println(instant);
        System.out.println(localDate);
        System.out.println(localTime);
        System.out.println(localDateTime);
        System.out.println(zonedDateTime);
    }
}
```

![image-20211120164649360](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120164649360.png)

JDK8.0 中新提供的日期 API 也可以与 `Date` 类进行转换。当然，在转换时需要借助一些工具类:

```java
import java.util.Date;

public class TestNewDate2 {
    public static void main(String[] args) {
        ZoneId zoneId = ZoneId.systemDefault();
        LocalDate localDate = LocalDate.now();  // 日期
        System.out.println(localDate);
        ZonedDateTime zdt = localDate.atStartOfDay(zoneId);
        Date date = Date.from(zdt.toInstant());
        System.out.println(zoneId);
        System.out.println(zdt);
        System.out.println("LocalDate:" + localDate);
        System.out.println("Date:" + date);
    }
}

```

![image-20211120165939848](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120165939848.png)

**SimpleDateFormat**

Date 默认支持的是西方国家的时间格式，如`Fri Nov 27 09:28:06 UTC 2020`。能否自定义 Date 的输出格式呢？使用 SimpleDateFormat 类就可以做到。

在 SimpleDateFormat 中，是通过构造方法指定 Date 的输出格式的，并且在设置这些格式时需要使用时间通配符，常见的通配符如下表所示。

| 通配符 | 含义 |
| ------ | ---- |
| y      | 年   |
| M      | 月   |
| d      | 日   |
| H      | 时   |
| m      | 分   |
| s      | 秒   |

例如`yyyy-MM-dd HH:mm:ss`就代表了“4 位数年-2 位数月-2 位数日 2 位数时:2 位数分:2 位数秒”的日期显示格式，详见以下程序。

```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class TestSimpleDateFormat1 {
    public static void main(String[] args) {
        Date date = new Date();
        String strDateFormat = "yyyy-MM-dd HH:mm:ss";
        SimpleDateFormat sdf = new SimpleDateFormat(strDateFormat);
        System.out.println(sdf.format(date));
    }
}
```

![image-20211120170553252](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120170553252.png)

除了将 Date 以固定格式的形式输出以外，SimpleDateFormat 还可以通过 `format` 方法，将某个固定格式的字符串转换为一个 Date 类型，详见以下程序。

```java
package String字符串;

import java.text.SimpleDateFormat;
import java.util.Date;

public class TestSimpleDateFormat2 {
    public static void main(String[] args) throws Exception{
        String strDateFormat = "yyyy-MM-dd HH:mm:ss";
        SimpleDateFormat sdf = new SimpleDateFormat(strDateFormat);
        //将字符串"2020-06-11 17:00:00"转为Date类型
        Date date = sdf.parse("2020-06-11 17:00:00");
        System.out.println(date);
    }
}
```

![image-20211120171031736](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211120171031736.png)

需要注意的是，待转换字符串`2020-06-11 17:00:00`的格式必须和 SimpleDateFormat 构造方法中参数的形式保持一致。

### 7.类和对象

#### 1.类定义的语法形式：

```java
public class 类名｛
    //定义类属性
    属性1类型:属性1名;
    属性2类型:属性2名;
    …
    //定义方法
    方法1定义
    方法2定义
    …
｝
```

现在创建一个Student类:

```java
public class Student {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;
    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点，" + stuName + "正在写作业!";
    }

}
```

需要注意的是，这个类里面没有 `main` 方法，所以只能编译，不能运行。

定义好 `Student` 类后，就可以根据这个类创建（实例化）对象了。类就相当于一个模板，可以创建多个对象。创建对象的语法形式如下。

```java
类名 对象名 = new 类名();
```

创建对象时，要使用 new 关键字，后面要跟着类名（构造方法名），类名后的括号内可传递构造参数。

根据上面创建对象的语法，创建王云这个学生对象的代码如下。

```java
Student wangYun = new Student();
```

这里，只创建了 wangYun 这个对象，并没有对这个对象的属性赋值，考虑到每个对象的属性值不一样，所以通常在创建对象后给对象的属性赋值。在 Java 语言中，通过 `.` 操作符来引用对象的属性和方法，具体的语法形式如下。

```java
对象名.属性 ;
对象名.方法() ;
```

通过上面的语法形式，可以给对象的属性赋值，也可以更改对象属性的值或者调用对象的方法，具体的代码如下。

```java
wangYun.stuName ="王云";
wangYun.stuAge = 22;
wangYun.stuSex = 1;            //1代表男，2代表女
wangYun.stuGrade = 4;        //4代表大学四年级
wangYun.learn();            //调用学生听课的方法
wangYun.doHomework(22);        //调用学生写作业的方法，输入值22代表现在是22点
```

接下来通过创建一个测试类 `TestStudent`（这个测试类需要和之前编译过的 `Student` 类在同一个目录），来测试 `Student` 类的创建和使用，程序如下。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        wangYun.learn();
        String restring = wangYun.doHomework(22);
        System.out.println(restring);
    }
}
```

![image-20211121130608150](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121130608150.png)

这个程序虽然非常简单，但却是我们第一次使用两个类来完成程序。其中 `TestStudent` 类是测试类，测试类中包含 `main` 方法，提供程序运行的入口。在 `main` 方法内，创建 `Student` 类的对象并给对象属性赋值，然后调用对象的方法。

这个程序有两个 Java 文件，每个 Java 文件中编写了一个 Java 类，编译完成后形成 2 个 class 文件。也可以将两个 Java 类写在一个 Java 文件里，但其中只能有一个类用 public 修饰，并且这个 Java 文件的名称必须用这个 public 类的类名命名，详见以下程序。

```java
public class TestStudent2 {
    public static void main(String[] args) {
        Student2 wangYun = new Student2();
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);
    }
}

class Student2 {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;
    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点，" + stuName + "正在写作业！";
    }
}
```

![image-20211121131213212](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121131213212.png)

在上面的例子中，对对象的属性都是先赋值后使用，如果没有赋值就直接使用对象的属性，会有什么样的结果呢？

下面将 `TestStudent` 测试类的代码修改成下面的代码。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        System.out.println("未赋值前的学生姓名为:" + wangYun.stuName);
        System.out.println("未赋值前的学生年龄为:" + wangYun.stuAge);
        System.out.println("未赋值前的学生性别数值为:" + wangYun.stuSex);
        System.out.println("未赋值前的学生年纪为:" + wangYun.stuGrade);
        wangYun.stuName = "王云";
        wangYun.stuAge = 22;
        wangYun.stuSex = 1;
        wangYun.stuGrade = 4;
        System.out.println("赋值后的学生姓名为：" + wangYun.stuName);
        System.out.println("赋值后的学生年龄为：" + wangYun.stuAge);
        System.out.println("赋值后的学生性别数值为：" + wangYun.stuSex);
        System.out.println("赋值后的学生年级为：" + wangYun.stuGrade);
    }
}
```

![image-20211121131510640](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121131510640.png)

从程序运行结果可以看出，在未给对象属性赋值前使用属性时，属性使用的都是对应数据类型的默认值，即如果该属性为引用数据类型，其初始默认值为 null，如果该属性是 int 型，其初始默认值为 0。

```java
import java.util.Scanner;

public class TestStuTea {
    static Scanner input = new Scanner(System.in);

    public static void main(String[] args) {
        Teacher[] tea = new Teacher[2];
        Student[] stu = new Student[4];
        for (int i = 0; i < tea.length; i++) {
            System.out.println("请创建并输入第" + (i + 1) + "个老师的基本信息");
            tea[i] = createTeacher();
        }
        for (int i = 0; i < stu.length; i++) {
            System.out.println("请创建并输入第" + (i + 1) + "个学生的基本信息");
            stu[i] = createStudent();
        }
        tea[0].teach();
        for (int j = 0; j < stu.length; j++) {
            stu[j].learn();
        }
        for (int j = 0; j < stu.length; j++) {
            String tempStr = stu[j].doHomework(20);
            System.out.println(tempStr);
        }
        for (int j = 0; j < stu.length; j++) {
            tea[1].checkHomework(stu[j]);
        }
    }

    public static Teacher createTeacher() {
        Teacher tea = new Teacher();
        System.out.print("请输入老师的姓名：");
        tea.teaName = input.next();
        System.out.print("请输入老师的专业：");
        tea.teaSpecialty = input.next();
        System.out.print("请输入老师的所讲授的课程：");
        tea.teaCourse = input.next();
        System.out.print("请输入老师的教龄：");
        tea.teaYears = input.nextInt();
        return tea;
    }

    public static Student createStudent() {
        Student stu = new Student();
        System.out.print("请输入学生姓名：");
        stu.stuName = input.next();
        System.out.print("请输入学生年龄：");
        stu.stuAge = input.nextInt();
        System.out.print("请输入学生性别数值（1代表男、2代表女）：");
        stu.stuSex = input.nextInt();
        System.out.print("请输入学生年级：");
        stu.stuGrade = input.nextInt();
        return stu;

    }


}


class Teacher {
    String teaName;
    String teaSpecialty;
    String teaCourse;
    int teaYears;

    public void teach() {
        System.out.println(teaName + "正在辛苦讲:" + teaCourse + "课程！");
    }

    public void checkHomework(Student stu) {
        System.out.println("讲授:" + teaCourse + "课程的老师:" + teaName + "已经批改完毕:" + stu.stuName + "的作业！");
    }
}

class Student {
    String stuName;
    int stuAge;
    int stuSex;
    int stuGrade;

    public void learn() {
        System.out.println(stuName + "正在认真听课！");
    }

    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点" + stuName + "正在写作业！";
    }
}
```

![image-20211121134200542](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121134200542.png)

![image-20211121134217478](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121134217478.png)

#### 2.初识封装

封装的目的是简化编程和增强安全性。

1. 简化编程是指，封装可以让使用者不必了解具体类的内部实现细节，而只是要通过提供给外部访问的方法来访问类中的属性和方法。例如 Java API 中的 `Arrays.sort()`方法，该方法可以用于给数组进行排序操作，开发者只需要将待排序的数组名放到 `Arrays.sort()`方法的参数中，该方法就会自动的将数组排好序。可见，开发者根本不需要了解 `Arrays.sort()`方法的底层逻辑，只需要简单的将数组名传递给方法即可实现排序。
2. 增强安全性是指，封装可以使某个属性只能被当前类使用，从而避免被其他类或对象进行误操作。例如在 `Student.java` 的程序中，`Student` 的 `stuAge` 属性是 `public` 的形式体现的，但这样做实际存在着安全隐患：`TestStudent` 类（或在访问修饰符可见范围内的其他类）完全可以随意的对 `stuAge` 进行修改，如以下程序。

```java
public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student();
        wangYun.stuAge = -10;
        ...
    }
}
```

如上，给 `stuAge` 赋了一个不符合逻辑的值，但语法是却正确的。因此这种做法，实际就给程序造成了安全问题。如何避免此类问题呢？使用 `private` 修饰符来修饰 `stuAge` 属性，以此禁止 `Student` 以外的类对 `stuAge` 属性的修改。但这么做未免显得“过犹不及”，为了保证安全，也不至于让其他类无法访问吧！有没有一种办法，既能让其他类可以访问 `Student` 类中的 `stuAge` 属性，又能保证其他类始终是在安全的数值范围内修改 `stuAge` 值呢？有，先用 `private` 修饰 `stuAge` 属性，然后再给该属性提供两个 `public` 修饰的、保证属性安全的访问方法（`setter` 方法和 `getter` 方法），即：

1. 用 `private` 禁止其他类直接访问属性；
2. 给 1 中的属性新增两个 `public` 修饰的 `setter` 和 `getter` 方法，供其他类安全的访问。

`setter` 方法用于给属性赋值，而 `getter` 访问用于获取属性的值。并且一般而言，`setter` 方法的名字通常是 `set+属性名`，`getter` 方法的名字通常是 `get+属性名`。

根据以上描述，先用 `private` 修饰 `stuAge`，禁止 `TestStudent` 类对 `stuAge` 的直接访问，以此保证 `stuAge` 安全性；然后新增 `setStuAge()`和 `getStuAge()`方法，一方面供 `TestStudent` 类间接的访问 `stuAge` 属性，另一方面也保证了 `stuAge` 的数据安全，详见以下程序。

```java
public class StudentPrivate {
    private int stuAge;

    public int getStuAge() {
        return stuAge;
    }

    public void setStuAge(int age) {
        if (age > 0 && age < 110)
            stuAge = age;
        else
            age = 0;
    }
}
```

后续，其他类只需要调用 setStuAge()和 getStuAge()方法，就能对 stuAge 属性进行安全的赋值或取值，代码如下。

```java
public class TestStudent3 {
    public static void main(String[] args) {
        StudentPrivate wangYun = new StudentPrivate();
        wangYun.setStuAge(-10);
        int age = wangYun.getStuAge();
        System.out.println(age);
        wangYun.setStuAge(22);
        age = wangYun.getStuAge();
        System.out.println(age);

    }
}
```

![image-20211121135113210](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121135113210.png)

实际上，使用 setter 和 getter 的解决方案用到了一个程序设计的基本原则：逻辑代码不能写在变量中，而必须写在方法或代码块中。

#### 3.构造方法基本语法

构造方法不同于普通方法，普通方法代表对象的行为，而构造方法是提供给系统用于创建对象的方法。

构造方法（也称为构造函数）是一种特殊的方法，它具有以下特点。

- 构造方法的方法名必须与类名相同。
- 构造方法没有返回类型，在方法名前不声明返回类型（包括 void）。

构造方法的语法形式如下。

```java
[访问修饰符] 类名([参数列表]) ;
```

虽然构造方法在语法形式上没有返回类型，但其实构造方法是有返回值的，返回的是刚刚被初始化完成的当前对象的引用。既然构造方法返回被初始化对象的引用，为什么不写返回值类型呢？例如 Student 类构造方法为什么不写成 `public Student Student（参数列表）｛…｝`呢？

因为 Java 设计人员把这种方法名（类名）和返回类型的类名相同的方法看成一个普通方法，只是名称“碰巧”相同罢了，编译器识别时也会认为它是一个方法。为了和普通方法进行区别，Java 设计人员规定构造方法不写返回值，编译器通过这一规定识别构造方法，而不是说构造方法真的没有返回值。

将 `Student` 类的代码改为下面的形式：

```java
private String stuName;
private int stuAge;
private int stuSex;
private int stuGrade;

public StudentInit (String name,int age,int sex,int grade) {
    stuName = name;
    stuAge = age;
    stuSex = sex;
    stuGrade = grade;
}
public void learn() {
    System.out.println(stuName + "正在认真听课！");
}

public String doHomework(int hour) {
    return "现在是北京时间：" + hour + "点" + stuName + "正在写作业！";
}
```

测试类 `TestStudent1.java` 的代码如下所示。

```java
public class TestStudent1 {
    public static void main(String[] args) {
        StudentInit wangYun = new StudentInit("王云",22,1,4);
        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);
    }
}

```

![image-20211121141633416](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121141633416.png)

#### 4.this关键字

`this` 是 Java 的一个关键字，它表示“指向当前对象的引用（后文简称为‘当前对象’）”。举个例子，在前面小节中给 `stuAge` 属性赋值的语句是`wangYun.setStuAge(22);`，这条语句中的当前对象就是 wangYun，因此在 `setStuAge()`方法中 `this` 就是 wangYun。

在实际开发时，this 通常用于以下两个场景。

1. 区分成员变量和局部变量，避免命名的烦恼。
2. 调用其他构造方法。

先看一下如何使用 this 区分成员变量和局部变量。在前面一小节中，我们是通过以下代码给 stuAge 赋值的。

```java
private int stuAge ;
...
public void setStuAge(int age) {
...
stuAge = age ;
}
```

是否可以将参数 `age`，和成员变量 `stuAge` 设置为相同的名称，如下所示。

```java
private int age ;
...
public void setAge(int age) {
...
age = age ;
}
```

显然，编译器将无法区分`age = age`这句代码中哪个变量是成员变量，哪个变量是参数，因此我们之前就只能通过不同的变量名来区分。而现在，我们就可以通过 this 来区分不同的 age，如下所示。

```java
private int age ;
...
public void setAge(int age) {
...
this.age = age ;
}
```

在`this.age = age ;`这句代码中，因为 this 代表着当前对象，因此`this.age`就代表了当前对象的 age 属性；而`age`没有 this 修饰，就会根据变量的作用域，默认为方法参数中的 age。

再看一下如何使用 this 调用其他构造方法。

在构造方法中，还可以使用 this 调用类中的其他构造方法，但这种`this()`语句必须写在构造方法的一行，如下所示。

```java
public Student() {
    //调用有一个String参数的构造方法
    this(" WangYun" );
}

public Student(String name) {
    //调用有两个参数的构造方法
    this(name,23);
}

public Student(String name, int age) {
    ...
}
```

需要注意的是，所有的构造方法之间不能循环调用，否则会出现类似“死循环”的现象。例如以上代码，如果在最后一个构造方法的第一行也加上`this()`，那么三个构造方法就会无限制的彼此调用。

例：

构造方法的主要作用是完成对象的初始化工作，它能够把定义对象时的参数传给对象。一个类可以定义多个构造方法，但需要根据参数的个数、类型或排列顺序来区分不同的构造方法，详见以下程序。

新建一个 `Student1.java` 文件，并输入以下代码。

```java
public class Student1 {
    private String name;
    private int age;
    private int sex;
    private int grade;

    public Student1(String name, int age, int sex, int grade) {
        this(name, age, sex);
        this.grade = 4;
    }

    public Student1(String name, int age, int sex) {
        this(name, sex);
        this.age = age;
        this.grade = 4;
    }

    public Student1(String name, int sex) {
        this.sex = sex;
        this.name = name;
        this.age = 22;
        this.grade = 4;
    }

    public Student1(String name) {
        this.name = name;
        this.age = 22;
        this.grade = 4;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setSex(int sex) {
        this.sex = sex;
    }

    public int getGrade() {
        return grade;
    }
    public void setAge(int age) {
        if (age > 0 && age <110) {
            this.age = age;
        } else {
            this.age = 0;
        }
    }
    public void learn() {
        System.out.println(name + "正在认真听课！");
    }
    public String doHomework(int hour) {
        return "现在是北京时间：" + hour + "点," + name + "正在写作业！";
    }
}
```

新建测试类 `TestStudent3`，其代码如下。

```java
public class TestStudent4 {
    public static void main(String[] args) {
        Student1 wangYun = new Student1("王云",22,1,4);
        Student1 liuJT = new Student1("刘静涛",21,2);
        Student1 nanTH = new Student1("南天华");
        nanTH.setSex(1);

        wangYun.learn();
        String rstString = wangYun.doHomework(22);
        System.out.println(rstString);

        liuJT.learn();
        System.out.println(liuJT.getName() + "正在读大学" + liuJT.getGrade() + "年级");
        System.out.println(nanTH.doHomework(23));
    }
}

```

![image-20211121143637588](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121143637588.png)

构造方法有一个约定：如果在定义类时没有定义构造方法，编译系统会自动插入一个无参数的默认构造方法，这个构造方法不执行任何代码。如果在定义类时定义了有参的构造方法，没有显式地定义无参的构造方法，那么在使用构造方法创建类对象时，则不能使用默认的无参构造方法。

例如，在 `TestStudent3` 程序的 `main` 方法内添加一行语句`Student leiJing = new Student();`，编译器会报错，提示没有找到无参的构造方法。

#### 5.对象的初始化过程

对象的初始化，实际就是先在堆内存中申请一块用于存放对象属性值的空间，然后再给这些属性值赋上默认值、程序员期望的数据或者用户指定的数据。当堆内存中的这块空间有了值以后，再在栈空间中申请一块空间并存放引用变量，然后用栈中的引用变量指向堆中的对象，最终就可以通过栈中的引用变量访问或者修改堆中的对象了，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/a52bd58b463cfe98caf9b39735b00a2a-0)

下面我们结合代码，分析对象初始化过程中内存演变的细节。

本次在堆中存放的对象是由 `Student` 类生成的，并且 `Student` 类通过初始化块给属性赋了值（初始化块会在本节的后续分析内存演变时讲解），详见以下程序。

```java
public class Student2 {
    private String name = "";
    private int age = -1;
    private int sex = -1;
    private int grade = -1;
    {
        System.out.println("使用初始化快初始化");
        this.name = "雷静";
        this.age = 22;
        this.sex = 2;
        this.grade = 4;
    }
    public Student2() {
        System.out.println("使用无参构造函数初始化");
    }

    public Student2(String name,int age,int sex,int grade) {
        System.out.println("使用有参构造函数初始化");
        this.name = name;
        this.age = age;
        this.sex = sex;
        this.grade = grade;
    }
    public void setSex(int sex) {
        this.sex = sex;
    }
    public int getGrade() {
        return grade;
    }
    public String getName() {
        return name;
    }
}
```

新建测试类 `TestStudent5.java`，其代码如下。

```java
public class TestStudent5 {
    public static void main(String[] args) {
        Student2 temp = new Student2();
        System.out.println(temp.getName() + "正在读大学" + temp.getGrade() + "年级");
        Student2 wangYun = new Student2("王云",22,1,4);
        System.out.println(wangYun.getName() + "正在读大学" + wangYun.getGrade() + "年级");
    }
}
```

对象初始化时的内存演变过程如下。

1. `Student2 temp= new Student2();`执行时，首先需要在堆内存中申请空间，用于存放对象的实例，这片空间上成员变量的值全部为默认值：name 的值是 null、age 的值是 0……，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/3b1d455c641443828bc109ede4544c83-0)

1. 紧接着，执行声明初始化（由设计该类的开发者指定），例如在 `Student2` 类中`private int age = -1;`代表程序员希望 age 属性用值-1 覆盖默认值，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/280c2be5a7e237b5ec4f52079256dcba-0)

3.初始化块初始化。

初始化块就是在类的下一级（与成员变量和成员方法同级）用一对大括号括起来的代码块，语法形式如下：

```java
{
    代码块
}
```

初始化块可以用来覆盖类的成员变量的值，初始化块的执行时机是发生在“声明初始化”之后，在“构造器初始化”之前。例如，如下的初始化代码，就用于给成员变量再次赋值，如图所示。

```java
{
    this.name = "雷静";
    this.age = 22;
    this.sex = 2;
}
```

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/1b9536540928bd247b6911a4f0207daa-0)

执行程序后，运行结果如图所示。大家可以通过运行结果，分析刚才说的初始化块的执行时机。

![image-20211121151010497](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121151010497.png)

1. 构造器初始化，例如`Student2 temp = new Student2("王云", 22, 1, 4);`，在默认初始化，声明初始化，初始化块之后，再此用构造器覆盖各个属性的值，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/a1eadb542a26b2ff6252e679101ed970-0)

#### 6.重载基本语法

在同一个类中，可以有两个或两个以上的方法具有相同的方法名，但它们的参数列表不同。这种形式被称为重载（overload）。所谓参数列表不同包括以下三种情形。

- 参数的数量不同。
- 参数的类型不同。
- 参数的顺序不同。

必须注意的是，仅返回值不同不能视为方法重载，还会得到一个语法错误。而且重载的方法之间只是“碰巧”名称相同罢了，不具备连带效应。既然方法名称相同，在使用相同的名称调用方法时，编译器怎么确定调用哪个方法呢？这就要靠传入参数的不同确定具体调用哪个方法。

注意，一个类的多个构造方法被视为重载，因为多个构造方法的方法名相同，而参数列表不同，符合重载的定义。

看以下程序中的代码，其中的重点是 `learn` 方法的重载。

```java
public class Student3 {
    private String name;
    private int age;

    public Student3(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void read(String bookName, String bookAuthor, double bookPrice) {
        if (bookName != null && bookAuthor == null && bookPrice != 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，书价：" + bookPrice);
        }
        //当bookPrice使用的是默认值时
        if (bookName != null && bookAuthor != null && bookPrice == 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，作者：" + bookAuthor);
        }

        //当全部的参数都使用的是默认值时
        if (bookName == null && bookAuthor == null && bookPrice == 0.0) {
            System.out.println(this.name + "正在读书");
        }

        //当全部的参数都使用的不是默认值时
        if (bookName != null && bookAuthor != null && bookPrice != 0.0) {
            System.out.println(this.name + "正在读《" + bookName + "》，作者：" + bookAuthor
                    + "，书价：" + bookPrice);
        }
    }

    public void read(String bookName, String bookAuthor) {
        this.read(bookName, bookAuthor, 0.0);
    }

    public void read(String bookName, double bookPrice) {
        this.read(bookName, null, bookPrice);
    }

    public void read(String bookName) {
        this.read(bookName, null, 0.0);
    }

    public void read() {
        this.read(null, null, 0.0);
    }

}

```

测试类 `TestStudent6.java` 文件代码如下。

```java
public class TestStudent6 {
    public static void main(String[] args) {
        Student3 stu = new Student3("王云",22);
        stu.read("Java编程思想","埃克尔",108.0);
        stu.read("Java编程思想","埃克尔");
        stu.read("Java编程思想",108.0);
        stu.read();
    }
}
```

![image-20211121152059252](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211121152059252.png)

#### 7.静态代码块、普通代码块、构造方法

```java
public class TestStatic {
    public TestStatic(){
        System.out.println("构造方法！");
    }
    static {
        System.out.println("静态代码块");
    }

    {
        System.out.println("普通代码快块");
    }

    public static void main(String[] args) {
        TestStatic a = new TestStatic();
        TestStatic b = new TestStatic();
        TestStatic c = new TestStatic();
    }
}

```

![image-20211122191737657](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211122191737657.png)

​		静态代码块只在类第一次创建对象的时候会执行，而且先于普通代码块和无参构造方法，再创建其他对象静态方法就不会再执行了。

​		普通代码块先于无参构造方法。

#### 8.方法的重写

![image-20211122193142973](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211122193142973.png)

> 父类有一个方法，子类重写了一编。

要求:

1. 方法名相同
2. 参数列表也相同

```java
public class TestReload {
    public static void main(String[] args) {
        Son son = new Son();
        son.eat();
    }
}


class Father {
    public void eat() {
        System.out.println("父类eat");
    }
}

class Son extends Father {
    @Override   // 表示重写了父类的eat方法，可加可不加
    public void eat() {
        System.out.println("子类eat");
    }
}
```

![image-20211122192933830](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211122192933830.png)

### 8.包和访问控制

#### 1.包

> 作用和 文件夹/目录一致
>
> 1. 避免重名问题
>
> 2. 将类等资源 进行结构化存储
>
>    命名：一般为域名的反转

> 为了更好地组织类，Java 提供了包机制。包是类的容器，用于分隔类名空间。如果没有指定包名，所有的类都属于一个默认的无名包。Java 中将实现相关功能的类组织到一个包中。例如，Java 中通用的工具类，一般都放在 `java.util` 包中。 总的来说，包有以下三个方面的作用。
>
> 1. 提供了类似于操作系统树形文件夹的组织形式，能分门别类地存储、管理类，易于查找并使用类。
> 2. 解决了同名类的命名冲突问题。例如，学生王云定义了一个类，类名叫 `TestStudent`，学生刘静涛也定义了一个叫 `TestStudent` 的类。如果在同一个文件夹下，就会产生命名冲突的问题。而使用了包的机制，就可以把王云定义的类存放在 `wangyun` 包下，把刘静涛定义的类存放在 `liujingtao` 包下，之后就可以先通过 `wangyun` 和 `liujingtao` 这样的包名，区分不同的目录，然后再使用 `TestStudent` 访问两个包中各自的类，从而解决了命名冲突的问题。
> 3. 包允许在更广的范围内保护类、属性和方法。

#### 语法

程序员可以使用 `package` 关键字指明源文件中的类属于哪个具体的包，包的语法形式如下。

```java
package pkg1[．pkg2[．pkg3…]];
```

程序中如果有 package 语句，该语句一定是源文件中的第一条可执行语句，它的前面只能有注释或空行。另外，一个文件中最多只能有一条 package 语句，即只能把一个类放在一个包中。

包的名字应该有层次关系，各层之间以`.`分隔。

#### 命名规则

通常包名全部用小写字母，这与类名以大写字母开头且各单词的首字母亦大写的命名约定有所不同。关于包的命名，现在使用最多的规则是使用翻转的 internet 域名（不含 www、ftp 等访问协议）。例如 abc 公司的域名为 abc.com，该公司开发部门正开发一个名为 fly 的项目，在这个项目中有一个工具类的包，则这个工具包的包名可以为：`com.abc.fly.tools`。

#### 2.JDK中的包

JDK 类库中包含的众多类，就是使用包进行结构化分的。划分的形式就像在硬盘上嵌套有各级子目录一样，JDK 类库最高一级的包名是 `java` 和 `javax`，其下一级的包名有 `lang、util、net、io` 等，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/4153921c13f383520961c4ec75449c0f-0)

下面简要介绍 JDK 类库中不同包的主要功能。

- `java.lang`：lang 是 language 的简写，这个包提供 Java 语言的基础类，例如 String、Math、Integer、System 和 Thread 等。
- `java.util`：util 是 utility 的简写，组织了 Java 的工具类，包含集合、事件模型、日期和时间设置、国际化和各种实用工具类。
- `java.io`：io 是 input 和 output 的合并简写，指输入和输出，组织了数据流、序列化和文件系统相关的类。
- `java.net`：net 即网络，这个包组织了为实现网络应用程序而提供的类。
- `java.awt`：抽象窗口工具集(Abstract Window Toolkit)，包含用于创建用户界面和绘制图形图像的类。

#### 3.导入包

> java.lang中的所有公共类，都是由系统默认导入到程序中，不需要我们手动导入。

创建一个包`com.bd.test`,在其下面创建一个TestPackage.java，内容为:

```java
package com.bd.test;

public class TestPackage {
    public void show() {
        System.out.println("package com.bd.test");
    }
}
```

再在com包下创建一个TestImport.java,其内容为：

```java
package com;

public class TestImport1 {
    public static void main(String[] args) {
        TestPackage tp = new TestPackage();
        tp.show();

    }
}
```

此时代码是报错的：

因为TestImport和TestPackage不在同一个包内，导致找不到TestPackage类，此时需要导入包。

**解决办法1**

引用不同包中的类有两种方法，其中一种非常直观的方法就是使用完整类名引用类，即 **包名+类名**（也称为类的全限定名）。例如，将上面 `TestImport1` 类修改为如下的内容。

新建`TestImport2`内容如下：

```java
package com;

public class TestImport2 {
    public static void main(String[] args) {
        com.bd.test.TestPackage tp = new com.bd.test.TestPackage();
        tp.show();
    }
}
```

这样就解决了，运行结果如下：

![image-20211124171618364](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211124171618364.png)

**解决方法2**

使用类的全限定名的方法虽然直观，但书写的内容多，且当使用的类比较多时，编辑和阅读都非常困难，因此并不推荐。接下来采用导入包的形式引用类，导入包的语法形式如下。

```java
import 包名.类名;
```

这里的包名、类名既可以是 JDK 提供的包和类的名称，也可以是用户自定义的包名和类名。

如果要使用一个包中的多个类，可以使用 `import 包名.* ;` 的形式导入这个包中所有的类。不过，包的导入只能导入当前目录中的类，而不能导入其子目录中的类。例如在导入 `java.util.*` 时，只会导入 `java.util` 包中的所有类，但不能导入 `java.util.function` 包中的类。另外，`import` 语句需要放在 `package` 语句后，在类定义之前。

根据语法，修改如下：

```java
package com;

import com.bd.test.TestPackage;

public class TestImport3 {
    public static void main(String[] args) {
        TestPackage tp = new TestPackage();
        tp.show();
    }
}
```

#### 4.访问控制

如果有些类并不希望被其他类使用，有些属性和方法需要对外界不可见或仅在有限的范围内可见。如何能做到这样的访问控制呢？这就需要使用访问权限修饰符。

Java 语言中的访问权限修饰符有 4 种，但却只有 3 个关键字。因为不写访问权限修饰符时，在 Java 中被称为默认权限（包权限），用 `default` 代替，可写可不写。其他 3 个访问权限修饰符分别为 `private`、`protected` 和 `public`。

例如上面的程序中，TestPackage中类的访问权限修饰符为Public，如果将Public删掉，那么TestImportx中就会报错，因为一个类不加访问权限修饰符就是default，default只允许本包使用。

#### 5.对类成员的访问控制

对于类的成员（属性和方法）而言，4 种访问权限修饰符都可以使用。下面按照权限从小到大的顺序（即 private < 默认 < protected < public）。

**私有权限 private**

private 可以**修饰属性**、**构造方法**、**普通方法**。被 private 修饰的类成员只能在定义它们的类中使用，在其他类中都不能访问。

**默认权限 default**

不写任何权限关键字就代表使用默认权限，属性、构造方法、普通方法都能使用默认权限。默认权限也称为同包权限。同包权限的元素只能在定义它们的类中以及同包的类中被调用。

创建yi个Student.java文件：

```java
package com.bd.test;

public class Student {
    String strName;
    public Student(String name) {
        this.strName = name;
    }

    void showName() {
        System.out.println("学生姓名为：" + this.strName);
    }
}
```

注意showName为默认权限，

再创建一个TestStudent文件:

```java
package com;

import com.bd.test.Student;

public class TestStudent {
    public static void main(String[] args) {
        Student wangYun = new Student("王云");
        wangYun.showName();
    }
}
```

此时`wangYun.showName()`报错，因为两个程序不是同一个包，TestStudent类访问不到Student类的showName方法。

**受保护权限 protected**

protected 可修饰属性、构造方法、普通方法，能在定义它们的类中以及同包的类中调用被 protected 修饰的成员。如果有不同包中的类想调用它们，那么这个类必须是这些成员所属类的子类。关于子类及相关概念，将会在后续讲解继承的时候详细介绍。

**公共权限 public**

public 可以修饰属性、构造方法和普通方法。被 public 修饰的成员，可以在任何一个类中被调用，是权限最大的访问权限修饰符。

访问权限修饰符使用范围总结如下表所示。

| 修饰符    | 类内部 | 同一个包中 | 子类 | 任何地方 |
| --------- | ------ | ---------- | ---- | -------- |
| private   | Yes    |            |      |          |
| default   | Yes    | Yes        |      |          |
| protected | Yes    | Yes        | Yes  |          |
| public    | Yes    | Yes        | Yes  | Yes      |

#### 6.static关键字

对象的成员变量有两种级别的使用范围：对象级别和类级别。

我们之前是先通过类实例化一个对象，然后再通过 **对象名.变量名** 的形式访问。这种访问成员变量的形式，实际就是对象级别的访问形式。对象级别的成员变量只能在当前对象的范围内使用。例如 `Student` 类有一个 name 属性，并且 `Student` 类实例化了 student1 和 student2 两个对象，那么在 `student1.name="张三"` 只是给 student1 对象的 name 赋了值，并不会影响到 student2 中的 name 属性。也就是说，对象级别中的成员变量，在不同对象中是各自独立的。但如果想让多个不同的对象共享同一个变量，就需要使用类级别的成员变量了。

在类成员的声明前，加上 `static`（静态的）关键字，就能创建出类级别的成员变量。声明为 static 的变量称为静态变量或类变量。可以直接通过类名引用静态变量，也可以通过实例名来引用静态变量，但推荐采用前者，因为采用后者容易混淆静态变量和实例变量。静态变量与类相关联，类的所有实例共同拥有一个静态变量。例如，如果 `Student` 类中的 name 属性是用 static 修饰的，那么 student1 和 student2 就会共享这变量。

除了修饰变量以外，声明为 static 的方法称为静态方法或类方法，最常见的例子是 `main` 方法。和静态变量一样，静态方法也可以被类名直接引用。

此外，静态方法可以直接调用静态方法，访问静态变量，但是不能直接访问实例变量和实例方法。静态方法中不能使用 this 关键字，因为静态方法不属于任何一个实例。



**用 static 修饰类的成员变量**

用 static 修饰的类的成员变量是静态变量，对该类的所有实例来说，只有一个静态值存在，所有实例共享一个变量。静态变量的最大特点是：如果一个类中存在静态变量，那么不论这个类实例化出了多少个对象，JVM 也仅会给这个静态变量分配一次内存（即所有对象共享这个静态变量），分配内存的时机是在程序第一次调用类的时候。

创建一个TestStatic文件:

```java
package com;

public class TestStatic {
    public static void main(String[] args) {
        Stu wangYun = new Stu();
        wangYun.avgAge = 22;
        System.out.println("王云所在班的平均年龄为:" + wangYun.avgAge);
        Stu liuJT = new Stu();
        System.out.println("王云所在班平均年龄为：" + wangYun.avgAge);
        System.out.println("刘静涛所在班的平均年龄为：" + liuJT.avgAge);
    }
}

class Stu {
    public static int avgAge;
}
```

![image-20211124184442089](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211124184442089.png)

通过程序运行结果可以看出，所有 `Student` 类的实例 wangYun 和 liuJT 都共用了静态变量 avgAge，当给其中任何一个实例的静态变量赋值时，都是对这一个静态变量进行操作。

 **用 static 修饰类的成员方法**

用 static 修饰类的成员方法，表示该方法被绑定于类本身（即属于类级别的方法），而不是类的实例。

创建一个TestStatic2文件：

```java
package com;

public class TestStatic2 {
    public static void main(String[] args) {
        Student.showAvgAge();
        System.out.println("惊天变量输出所在班平均年龄为：" + Student.avgAge);
    }
}

class Student {
    public static int avgAge = 22;
    public static void showAvgAge() {
        System.out.println("静态方法输出所在班平均年龄为：22");
    }
}
```

![image-20211124184726848](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211124184726848.png)



注意，在 `TestStatic2` 程序的 `main` 方法中，都是通过`类名.静态变量名`和`类名.静态方法名`的形式访问静态变量和调用静态方法的。通过`类实例.静态变量`和`类实例.静态方法`也可以访问静态变量和调用静态方法，但不推荐使用。

**静态方法不能操作实例变量**

静态方法可以操作静态变量，不能操作实例变量.

#### 7.Java静态快

静态块的语法形式如下。

```java
static
{
    语句块
}
```

Java 类首次装入 JVM 时，会对静态成员或静态块进行一次初始化，注意此时还没有产生对象。因此，静态成员和静态块都是和类绑定的，会在类加载时就进行初始化操作。

之后，当类加载完毕后，才能实例化出对象，并在对象产生的同时对实例成员进行初始化。因此，实例成员是和对象绑定的，会在实例化对象时一并进行初始化。

```java
package com.bd.test;

public class Student1 {
    private static String staticName = "静态姓名";
    private String stuName = "";
    static {
        System.out.println("***使用静态初始化块初始化***");
        System.out.println("静态块里显示静态变量值：" + staticName);
    }
    {
        this.stuName = "雷静";
        System.out.println("使用初始化块初始化");
        System.out.println("普通块里显示实例变量值：" + stuName);
        System.out.println("普通块里显示静态变量值:" + staticName);
    }
    public Student1(String name) {
        this.stuName = name;
        System.out.println("***使用有参构造函数初始化***");
        System.out.println("构造方法里显示实例变量值：" + stuName);
        System.out.println("构造方法里显示静态变量值：" + staticName);
    }

    public static void main(String[] args) {
        Student1 stu = new Student1("王云");
        
    }
}
```

![image-20211124194113514](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211124194113514.png)

静态变量和静态块都是在类实例化对象前被执行的，而且只执行一次。

#### 8.单例模式

饿汉式与懒汉式步骤：

1. 构造器私有化 => 防止直接new
2. 类内部创建对象
3. 向外部暴露一个静态公共方法getInstance
4. 代码实现

**饿汉式与懒汉式区别**

1. 二者最主要的区别在于创建对象的时机不同：饿汉式是在类加载就创建了对象实例，而懒汉式是在使用时才创建。
2. 饿汉式不存在线程安全问题，懒汉式存在线程安全问题。
3. 饿汉式存在浪费资源的可能，因为如果程序员一个对象实例都没有使用，那么饿汉式创建的对象就浪费了，懒汉式是使用时才创建，就不存在问题。
4. JavaSE标准类中，java.lang.Runtime就是经典的单例模式。

![image-20211207175842979](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207175842979.png)

##### 1.饿汉式

> 饿汉式就是对象还没有用，就已经存在了。

```java
package Single_;


/**
 * @author Zhtao
 * @date 2021/12/7 17:37
 */
public class SingleTon01 {
    public static void main(String[] args) {
        GirlFriend gf = GirlFriend.getInstance();
        System.out.println(gf);
        GirlFriend gf2 = GirlFriend.getInstance();
        System.out.println(gf2);
    }
}


// 有一个类=> GirlFriend
// 只能有一个女朋友
class GirlFriend {
    private String name;
    // 为了在静态方法getInstance中返回gf，所以要设置为static。
    private static GirlFriend gf = new GirlFriend("小红红");

    // 1.将构造器私有化
    // 2. 在类内部直接创建对象,该对象是静态的
    // 3.提供一个静态公共方法，返回gf对象
    private GirlFriend(String name) {
        this.name = name;
    }

    public static GirlFriend getInstance() {
        return gf;
    }

    @Override
    public String toString() {
        return "GirlFriend{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

##### 2.懒汉式

> 使用的时候才创建对象

```java
package Single_;

/**
 * 单例模式-懒汉式
 *
 * @author Zhtao
 * @date 2021/12/7 17:47
 */
public class SingleTon02 {
    public static void main(String[] args) {
        Cat xiaomao = Cat.getInstance();
        System.out.println(xiaomao);
        Cat xiaomao2 = Cat.getInstance();
        System.out.println(xiaomao);
        System.out.println(xiaomao == xiaomao2);
    }
}

// 希望程序在运行中，只能创建一个Cat对象
// 单例模式
class Cat {
    private String name;
    private static Cat cat;

    // 步骤
    // 1.将构造器私有化
    // 2.定义一个static静态属性对象
    // 3.提供一个公共的static方法，可以返回一个Cat对象
    private Cat(String name) {
        this.name = name;
    }

    public static Cat getInstance() {
        if (cat == null) { // 如果没有创建对象
            cat = new Cat("小可爱");
        }
        return cat;
    }

    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

![image-20211207175354111](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207175354111.png)

****

单例模式是指：无论创建了多少个引用，在堆中仅仅只有一个实例对象，如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/16df97061e276bb817a8d92c968b40e7-0)

实现单例模式的核心思路是将构造方法私有化，即使用 private 修饰构造方法，然后利用 static 成员变量的“一次性”，如下所示。

```java
public class Singleton {
    private Singleton() {
    }
}
```

这样做的目的，就是为了防止其他类直接通过构造方法实例化多个对象，从而破坏单例模式的规则。但显然，使用 private 将构造方法“屏蔽”后，其他类就得另想办法获取 Singleton 的对象。通常，可以给该类再设置一个私有的 Singleton 属性，然后通过 getter 方法限制只能实例化出一个 Singleton 对象，并将此对象暴露给外部的类访问，详见以下程序所示。

创建Singletonwe文件：

```java
package 包和访问控制;

public class Singleton {
    private static Singleton instance;
    private Singleton() {

    }
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

之后，不论有多少对象调用 `getInstance()`方法，实际都只返回了同一个实例（因为静态成员 instance 只有 1 份，而且根据代码逻辑，一旦 instance 非 null，就不再创建新对象），详见以下程序。

在Singleton文件下方添加：

```java
class TestSingleton {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2);
    }
}
```

![image-20211124194932634](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211124194932634.png)

证明只创建了一个Singleton对象。

### 9.面向对象的基本特征

> - 封装就是将抽象得到的属性和方法结合起来，形成一个有机的整体——类。类里面的一些属性，需要隐藏起来，不希望直接对外公开，但同时也提供了供外部访问的方法（setter 和 getter 方法），用于访问这些需要隐藏的属性
>
> - 继承可以使得子类沿用父类的成员（属性和方法）。当多个子类具有相同的成员时，就可以考虑将这些成员提取出来，放到父类中，然后再用子类去继承这个父类，也就是将一些相同的成员提取到了更高的层次中。

#### 1.继承

 继承的关键字是 `extends`，语法形式如下。

 ```
class A extends B{
    类定义部分
}
 ```

 以上表示 A 类继承 B 类，B 类称为父类、超类或基类；A 类称为子类、衍生类或导出类。 例如可以将 `Car` 类和 `Truck` 类重复的代码挑出来，提取到一个单独的 `Vehicle` 类中，即将 `Vehicle` 类作为 `Car` 类和 `Truck` 类的父类，然后让 `Car` 类和 `Truck` 类继承 `Vehicle` 类，这样 `Car` 类和 `Truck` 类就可以直接沿用 `Vehicle` 类的属性和方法。

例：

```java
package 面向对象基本特征;

public class Vehicle {
    String name = "汽车";    //车名
    int oil = 20;            //油量
    int loss = 0;            //车损度

    //无参构造方法
    public Vehicle() {
    }

    //构造方法，指定车名
    public Vehicle(String name) {
        this.name = name;
    }

    //加油
    public void addOil() {
        if (oil > 40)                //如果加油20升则超过油箱容量，则加到60升即可
        {
            oil = 60;
            System.out.println("邮箱已加满!");
        } else {                //加油20升
            oil = oil + 20;
        }
        System.out.println("加油完成!");
    }

    //行驶
    public void drive() {
        if (oil < 10) {
            System.out.println("油量不足10升，需要加油！");
        } else {
            System.out.println("正在行驶!");
            oil = oil - 5;
            loss = loss + 10;
        }
    }
}
```

```java
package 面向对象基本特征;

public class Car1 extends Vehicle{
}

class TestCar {
    public static void main(String[] args) {
        Car1 car = new Car1();
        System.out.println(car.name);
        car.drive();

    }
}
```

![image-20211125201109729](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125201109729.png)

虽然 `Car` 类没有定义任何内容，但却可以使用父类 `Vehicle` 提供的属性和方法，这就是继承的作用。

使用继承是否能够获取父类的一切内容呢？不是，以下是两种特殊的情况。

- 子类无法继承父类的构造方法。

  构造方法是一种特殊的方法，子类无法继承父类的构造方法。

- 子类不能继承父类中不符合访问权限的成员。

我们知道，private 修饰的成员仅对当前类可见，而继承是子类继承父类的成员，显然子类和父类是不同的类，因此子类无法继承父类中用 private 修饰的成员。同理，子类也无法继承父类中不满足 protected 或默认访问权限修饰的成员。如果将父类 Vehicle 中的 name 属性用 private 修饰，并用子类继承此属性，那么编译时就会报错。

#### 2.方法重写

有的时候，父类继承而来的方法不能满足子类的需要，此时就可以在子类中对父类的同名方法进行覆盖，这就是重写。

```java
package 面向对象基本特征;

public class Truck1 extends Vehicle {
    private String load = "10吨";            //吨位

    //构造方法，指定车名和吨位
    public Truck1(String name, String load) {
        this.name = name;
        this.load = load;
    }

    //获取吨位
    public String getLoad() {
        return load;
    }

    //显示车辆信息
    public void show() {
        System.out.println("显示车辆信息：\n车辆名称为：" + this.name + " 吨位是："
                + this.load + " 油量是：" + this.oil + " 车损度为：" + this.loss);
    }

    //子类重写父类的drive( )方法
    public void drive() {
        if (oil < 15) {
            System.out.println("油量不足15升，需要加油！");
        } else {
            System.out.println("正在行驶!");
            oil = oil - 10;
            loss = loss + 10;

        }
    }
}
```

```java
package 面向对象基本特征;

public class TestZuChe3 {
    public static void main(String[] args) {
        Truck1 truck1 = new Truck1("大力士二代","10吨");
        truck1.show();
        truck1.drive();
        truck1.show();
        truck1.drive();
        truck1.drive();
        truck1.drive();
        truck1.addOil();
        truck1.show();
    }
}
```

![image-20211125201753877](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125201753877.png)

通过上面的例子可知，当子类的某个行为特征与父类不同时，就可以通过重写来覆盖父类已有的方法。此外，子类也可以扩展父类的成员，即子类可以根据自身需求，额外的增加一些成员。

```java
package 面向对象基本特征;

public class Car1 extends Vehicle{
    String brand = "红旗";

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }
}

class TestCar {
    public static void main(String[] args) {
        Car1 car = new Car1();
        car.setBrand("长城");
        System.out.println("品牌" + car.brand);
        car.oil = 5;
        car.drive();
//        System.out.println(car.name);
//        car.drive();

    }
}
```

在子类 `Car` 中新增了 `brand` 属性和 `getBrand()`及 `setBrand()`方法，之后子类 `Car` 既可以使用自身定义的属性和方法，也可以使用从父类继承而来的属性和方法。

是不是父类中的所有方法都能被子类重写呢？不是。如果父类中的某个方法是被 `final` 修饰的，则这个方法就不能被子类重写。

- final 修饰的变量，变量值不能被改变。
- final 修饰的类，不能被继承。
- final 修饰的方法，不能被子类重写。

另外，重写在语法上需要满足如下条件。

- 重写方法与被重写方法同名，参数列表也必须相同。
- 重写方法的返回值类型必须和被重写方法的返回值类型相同或是其子类。
- 重写方法不能缩小被重写方法的访问权限。

#### 3.super关键字

目前 `Car` 类只定义了 `brand` 一个属性，但 `Car` 继承了 `Vehicle` 类。因此 `Car` 类能够使用的属性是由 `brand` 和 `Vehicle` 类中的属性两部分共同组成的。那么此时，子类 `Car` 的构造方法应该如何设计呢？换句话说，我们知道构造方法可以用于给属性赋初值，而构造方法又不能被子类继承，那么在使用了继承后，如何同时调用父类和子类的构造方法，从而给所有的属性赋值呢？可以使用 `super()`。

`super()` 可以调用父类的构造方法。但此时，必须将 `super()`写在子类构造方法的第一行，其语法形式如下。

```java
super( [参数列表] )
```


在Car1类中增加构造方法如下：

```java
public Car1(String name,String brand) {
        super(name);	//使用super关键字，调用父类的构造方法
        this.brand = brand;
    }
```

需要注意的是，子类的构造方法中如果不写 `super()`，编译器会帮助你在子类构造方法的第一行加上`super()`，因为在子类中调用父类构造器是“必须的”。但如果父类中只存在有参构造方法，并没有提供无参构造方法，则需要在子类构造方法中显式地调用父类存在的构造器。

简言之，子类构造方法中调用父类构造方法是“必须的”，如果程序员显式进行了调用，则编译器不提供额外帮助，如果程序员未通过 `super()`来调用，编译器就会帮助你插入`super()`，这时可能因为父类中没有无参构造器而得到一个编译错误。



**在子类构造方法第一行显式的通过`super([参数列表])`，调用父类的某一个有参构造方法，如下所示。**

```java
public class Sup {
    public Sup( String arg){          //父类中没有无参构造方法，只有有参构造方法
    }
}

class Sub extends Sup {
    public Sub(){
      super("argValue") ;           //显式的通过super([参数列表])，调用父类的有参构造方法
      // ..
    }
}
```

**先通过`this([参数列表])`调用本类中的其他构造方法，再在其他构造方法中通过`super([参数列表])`显式的调用父类的构造方法，如下所示。**

```java
public class Sup {
    public Sup( String arg){
    }
}

class Sub extends Sup {
    public Sub(){
        this(1) ;                    //先调用本类的其他构造方法
    }
    public Sub(int a){
        super("argValue") ;          //再调用父类的构造方法

    }
}
```

不难发现，以上形式的本质其实是一样的，都需要显式的写上`super([参数列表])`。

目前，我们可以通过继承直接沿用父类中已有的方法，并且通过方法重写覆盖父类中的方法。并且知道，当方法被重写以后，子类默认调用的是子类中重写后的方法，但如何调用父类中被重写的那个方法呢？使用 super 关键字，即可以使用 super 明确调用父类中的方法。 请看接下来的程序。

```java
package 面向对象基本特征;

public class Sup {
    public void info() {
        System.out.println("Sup 的info方法");
    }
}

class Sub extends Sup {
    public void info() {
        System.out.println("Sub 的info方法");
    }
    public void show() {
        info();
        super.info();
    }

    public static void main(String[] args) {
        Sub sub = new Sub();
        sub.show();
    }
}
```

因为子类 `Sub` 和父类 `Sup` 都定义了 `info()`方法，因此在子类 `Sub` 的 `show()`中，如果直接编写 `info()`或 `this.info()`，调用的就是 `Sub` 中的 `info()`方法；如果编写的是 `super.info()`，那么就会调用父类 `Sup` 中的 `info()`方法。

![image-20211125205457838](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125205457838.png)

在使用 super 明确调用父类中的方法时，一种常见的做法是，通过 super 对父类中已有的方法进行补充，如下所示，在子类的 `info()`方法中，先通过 super 调用父类的 `info()`，然后再进行一些额外的代码补充。

```java
class Sub extends Sup {
    public void info() {
        super.info();
        System.out.println("Sub 的info方法是对Sup的补充");
    }
    ····
}
```

现在，对于“在子类继承了父类后，子类继承父类的方法”这一问题总结如下：

1.  子类可以直接沿用父类的方法；
2.  子类可以重写父类的方法；
3.  子类可以在父类提供方法的基础上，额外新增一些功能。

**this和super的区别：**

1. this 代表当前对象本身，而 super 代表父类对象。
2. 使用 this 可以调用当前对象的属性或方法，使用 super 可以调用父类对象的属性或方法。
3. 使用 this 可以调用当前类中的其他构造方法，使用 super 可以调用父类中的构造方法。

**this和super联系：**

1. super 和 this 都指向一个对象，因此 super 和 this 的本质都是引用。二者都可以调用类或对象的属性、方法。
2. 在使用 super()或 this()调用构造方法时，都必须写在构造方法的第一行。因此，在一个构造方法内部，不可能同时使用 super()和 this()来调用其他的构造方法。

#### 4.继承中的初始化

父类、子类中的静态块、非静态块、构造方法的执行顺序：

```java
package 面向对象基本特征;

public class InitDemo {
    public static void main(String[] args) {
        System.out.println("第一次实例化子类：");
        new Sub1();
        System.out.println("第二次实例化子类：");
        new Sub1();
    }
}
class Super {
    static {
        System.out.println("父类中的静态块！");
    }
    {
        System.out.println("父类中的非静态块！");
    }
    Super() {
        System.out.println("父类构造方法！");
    }
}
class Sub1 extends Super {
    static {
        System.out.println("子类中的静态块！");
    }
    {
        System.out.println("子类中的非静态块！");
    }
    Sub1() {
        System.out.println("子类构造方法！");
    }
}
```

![image-20211125210200078](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125210200078.png)

通过运行结果可以看出，在第一次实例化子类时，先调用父类的静态块，再调用子类的静态块，之后再调用父类的非静态块和构造方法，再调用子类的非静态块和构造方法。这说明在第一次实例化某个类的对象时，该类的继承路径上的所有父类会被加载（伴随静态块被执行），然后是该类被加载。类加载完毕后，才可被实例化。接下来是，自上而下实例化，也就是说，即便没有显式实例化父类，父类也会实例化出对象。

另外，当第二次实例化子类时，父类和子类的静态块都不再被调用，再次说明静态成员初始化、静态块初始化都是在类加载时执行的。

#### 5.多态

多态可以优雅的解决程序中的扩展性问题。假设在租车系统中有一个 `drive(Car car)`方法，显然该方法只能传递一个 Car 类型的参数，因此如果想传递一个 Truck 类型的参数，就必须再重新编写一个 `drive(Truck truck)`方法。后续，随着项目的扩大，如果要给 `drive()`方法传递十种类型的参数，就需要根据参数类型编写十个重载的 `drive()`方法。但如果使用多态，这一问题就可以得到很好的解决。

根据继承的知识，可以给 Car 和 Truck 等各种类型的车设置一个共同的父类 `Vehicle`，之后只需要编写一个 `drive(Vehicle vehicle)`方法，就可以接收所有子类型的参数了，即可以使用 `Vehicle` 接收 `Car、Truck` 等各种子类型变量。实际上，Java 就是通过多态机制实现这一功能的。

在逻辑上，多态与继承类似，都符合`is a`的关系，例如`Car is a Vehicle `、`Truck is a Vehicle `等。显然，`is a`的左侧是子类，而右侧是父类。这种`is a`的逻辑，就保证了在形式上，父类引用可以指向子类对象，例如`Vehicle vehicle = new Car();`就是多态的一种典型写法。

在`Vehicle vehicle = new Car();`中，子类的 `Car` 对象赋值给了父类 `Vehicle` 引用，这称为向上转型；在引用 `vehicle` 上调用方法，在运行时刻究竟调用的是父类 `Vehicle` 中的方法还是子类 `Car` 中的方法呢？实际需要通过运行时的对象类型来判断，这称为动态绑定。向上转型和动态绑定就是多态的具体实现机制，以下通过“租车系统”逐步介绍。

**向上转型**

向上转型是指子类可以自动的转为父类对象，如 `父类 引用 =new 子类();` 就是多态的一种典型写法。

阅读“租车系统”的需求，发现程序中需要新建一个驾驶员（租车者）类 `Driver.java`，这个类有一个姓名的属性，还有两个获取车辆信息的方法，具体代码如下。

```java
package 面向对象基本特征;

public class TestZuChe4 {
    public static void main(String[] args) {
        Car car = new Car("战神", "长城");                //初始化轿车对象car
        Truck truck = new Truck("大力士二代", "10吨");    //初始化卡车对象truck
        Driver d1 = new Driver("柳海龙");                //创建并初始化驾驶员对象
        d1.callShow(car);                        //调用驾驶员对象相应的方法
        d1.callShow(truck);                        //调用驾驶员对象相应的方法
    }
}
```

![image-20211125212648338](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125212648338.png)

在写 `Driver` 类的过程中，驾驶员获取车辆信息的功能用了两个重载方法，如果要获取轿车信息，则输入的是轿车对象（如`d1.callShow(car);`），方法体内调用轿车对象的方法；如果要获取卡车信息，则输入的是卡车对象（如`d1.callShow(truck); `），方法体内调用卡车对象的方法。如果需要从 `Vehicle` 类继承出十种车辆类型，则在 Driver 类中需要写十个方法。这样的做法过于繁琐！

接下来用多态的方式解决这个问题。

首先要在 `Vehicle` 类中增加一个 `show()`方法，方法体为空，这样 `Car` 类和 `Truck` 类中的 `show()`方法实际是重写了 `Vehicle` 类中的 `show()`方法，代码如下。

```java
public class Vehicle {
    //省略其他代码
    //显示车辆信息
    public void show(){
    }
}
```

接下来修改 `Driver` 类，将原来两个 `callShow()`方法合并成一个方法，输入参数不再是具体的车辆类型，而是这些车辆类型的父类 `Vehicle`，在方法体内调用 `Vehicle` 的 `show()`方法，详见以下程序。

```java
//驾驶员（租车者）类
public class Driver {
    String name  = "驾驶员";            //驾驶员姓名
    //构造方法，指定驾驶员名
    public Driver(String name){
        this.name = name;
    }
    //获取驾驶员名
    public String getName(){
        return name;
    }
    //驾驶员获取车辆信息，输入参数为车对象
    public void callShow(Vehicle v){
        v.show();
    }
}
```

运行下面的测试程序，程序正常运行。

```java
class TestZuChe5
{
    public static void main(String[] args)
    {
        Car car = new Car("战神","长城");                //初始化轿车对象car
        Truck truck = new Truck("大力士二代","10吨");    //初始化卡车对象truck
        Driver d1 = new Driver("柳海龙");                //创建并初始化驾驶员对象
        d1.callShow(car);                        //调用驾驶员对象的相应方法
        d1.callShow(truck);                        //调用驾驶员对象的相应方法
    }
}
```

总结如下：

- 在父类 `Vehicle` 类中有 `show()`方法。
- 在子类 `Car` 类和 `Truck` 类中重写了 `show()`方法，实现了不同的功能。
- 在 `Driver` 类中，`callShow(Vehicle v)`方法的形参是一个父类对象的引用。
- 在测试类的代码中，`d1.callShow(car);`和 `d1.callShow(truck);`这两行语句调用 `callShow (Vehicle v)`方法时，实际传入的是子类对象，最终执行的是子类对象重写的 `show()`方法，而不是父类对象的 `show()`方法。

可见向上转型，实际就是父类的引用指向子类对象。也就是上面例子中 `Vehicle` 类的引用，指向了 `car` 和 `truck` 这两个对象。

向上转型的好处，不仅是在 `Driver` 类中不需要针对 `Vehicle` 类的多个子类写多个方法，减少了代码编写量，而且增加了程序的扩展性—在现有程序架构的基础上，可以再设计开发出若干个 `Vehicle` 类的子类（重写 `show()`方法），这样在不用更改 `Driver` 类的情况下，就可以通过在测试类中实例化新的 `Vehicle` 子类对象，并将这些子类对象传入 `Driver` 类的 `callShow(Vehicle v)`方法。

**动态绑定**

动态绑定是指在编译期间方法并不会和“引用”的类型绑定在一起，而是在程序运行的过程中，JVM 需要根据具体的实例对象才能确定此时要调用的是哪个方法。重写方法遵循的就是动态绑定。

例如，在程序 `Sup.java` 中，父类 `Sup` 和子类 `Sub` 都定义了 `info()`方法，此时执行以下代码。

```java
Sup x= new Sub() ;
x.info() ;
```

由于 `Sub` 类重写了 `Sup` 中的 `info()`方法，在编译期间 `info()`方法不会和任何一个具体的类绑定起来，而是在运行期间，会列举出 `Sub` 类中 `info()`的方法和从父类 `Sup` 继承过来的 `info()`方法，然后根据当前的实例对象是 `Sub` 对象，选择调用 `Sub` 类中的 `info()`方法。

有动态绑定，自然就有静态绑定。静态绑定是指程序编译期的绑定。以下的类信息，使用的就是静态绑定机制：

- `final`、`static` 或 `private` 修饰的方法，以及重载方法和构造方法。
- 成员变量。

**面向基类编程的思想**

在程序设计时，一种推荐的编程思想是“面向基类”编程。也就是建议将面向的“对象”抽象为更高层次的基类。例如不建议通过 `drive(Car car)`或 `drive(Truck truck)`等方法，限制方法接收的参数是某一个具体的对象类型，而建议将这些对象抽象成一个共同的基类，如 `drive(Vehicle vehicle )`，这样一来就可以利用多态的特性方便的对程序进行扩展，不必每增加一个具体的子类就得新增一个具体的方法。例如 `drive(Vehicle vehicle )`就可以接收任何 `Vehicle` 以及子类对象，因此可以大大减少代码的冗余度。

**向下转型**

向上转型虽然可以减少代码量，增加程序的可扩展性，但同时也有自身的问题。例如，在程序 `TestZuChe4.java` 中 `Driver` 类的 `callShow(Vehicle v)`方法中，只能调用 `Vehicle` 类的方法，不能调用 `Vehicle` 类子类特有的方法（例如 `Car` 类中 `getBrand()`方法），这就是向上转型的局限性。这个问题的解决办法就是向下转型。

顾名思义，向下转型就是将一个父类转换成一个子类的动作。但要注意的是，向下转型不是自动进行的，需要人为的进行强制类型转换。请看下面的程序例子。

```java
class TestZuChe6 {
    public static void main(String[] args) {
        Vehicle v = new Car("战神", "长城");    //声明父类对象，实例化出子类对象
        v.show();                        //实际调用子类重写父类的show()方法
        //System.out.println(v.getBrand());;        //编译错误，无法调用子类特有的方法
        Car car = (Car) v;                    //将对象v强制类型转换成Car类对象
        System.out.println(car.getBrand());        //调用Car类特有方法getBrand()
        Truck truck = (Truck) v;            //将对象v强制类型转换成Truck类对象
        System.out.println(truck.getLoad());    //调用Truck类特有方法getLoad()
    }
}
```

对象 v 是可以强制类型转换成 `Car` 类型的，因为它本身实例化的时候就是 `Car` 类型，所以可以进行强制类型转换，并且转换完后可以调用 `Car` 类特有的方法 `getBrand()`。但是对象 v 是不可以强制类型转换成 `Truck` 类型的，因为对象 v 实例化的时候是 `Car` 类型，把 `Car` 类型转换成 `Truck` 类型，会抛出异常（类型转换异常）。

程序员编程的过程中，在进行对象的强制类型转换时，如何保证转换的正确性呢？可以使用 Java 提供的 `instanceof` 运算符（不是方法）来进行预判断。`instanceof` 运算符的语法形式如下。

```java
对象 instanceof 类
```

该运算符判断一个对象是否属于一个类，返回值为 `true` 或 `false`。请看下面的例子。

```java
class TestZuChe7 {
    public static void main(String[] args) {
        //Vehicle v = new Car("战神","长城");        //声明父类对象，实例化出子类对象
        Vehicle v = new Truck("大力士二代", "10吨");
        v.show();
        if (v instanceof Car)                    //对象v属于Car类型
        {
            Car car = (Car) v;                    //将对象v强制类型转换成Car类对象
            System.out.println(car.getBrand());        //调用Car类的特有方法getBrand()
        } else {                            //对象v不属于Car类型
            Truck truck = (Truck) v;            //将对象v强制类型转换成Truck类对象
            System.out.println(truck.getLoad());    //调用Truck类的特有方法getLoad()
        }
    }
}
```

通过 `instanceof` 判断对象 v 属于哪个类，再进行强制类型转换，就可杜绝强制类型转换抛出异常，增加程序的健壮性。

**属性覆盖问题**

普通方法是在运行期间才动态绑定的，但成员变量（属性）是在程序编译期就完成绑定的。因此方法和属性在“覆盖”问题上是有所区别的，方法覆盖的问题（即方法重写)

```java
package 面向对象基本特征;

class Super1 {
    public int i = 50;
}

public class Sub2 extends Super1{
    public int i=100;

    public static void main(String[] args) {
        Sub2 sub2 = new Sub2();
        System.out.println(sub2.i);
    }
}
```

![image-20211125221333172](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125221333172.png)

程序运行的结果是 100，因为 Sub 对象自身拥有 i 属性，因此`sub.i`使用的就是 Sub 中的属性，这种情况通常也称为就近访问原则。将代码修改为以下内容。

```java
package 面向对象基本特征;

class Super1 {
    public int i = 50;
}

public class Sub2 extends Super1{
    public int i=100;

    public static void main(String[] args) {
        Super1 sup = new Sub2();
        System.out.println(sup.i);
    }
}
```

![image-20211125221528336](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211125221528336.png)





此时的程序运行结果是 50，因为属性 i 在编译期间就已经绑定在 `Super` 类了，并不会像普通方法那样在运行期间动态绑定，因此后续 `sup` 引用使用的就是 `Super` 类中绑定的属性 i。

- 当子类重写了父类的方法时，调用主体（即对象）和方法是运行时绑定的；
- 当子类和父类的属性重名时，调用主体（即对象）和属性是编译时绑定的。



**小结**

封装、继承和多态是面向对象的三大特征。多态让父类的引用既可以指向父类对象，也可以指向子类对象。在逻辑上，多态符合`is a`的关系，一种典型的多态写法就是`父类 引用 = new 子类()；`，例如`Vehicle vehicle = new Car();`，其`is a`关系就是`Car is a Vehicle`。

向上转型和动态绑定是多态的实现机制。向上转型是指子类对象可以自动的赋值给父类型的引用，而无需显式的转换；而动态绑定是指在程序运期间才将具体的实例对象和方法进行绑定。





### 10.抽象类和接口

#### 1.抽象类

> 在面向对象的世界里，所有的对象都是通过类来实例化的。但反之，所有的类都能用来实例化对象吗？答案是否定的。除了前面介绍的类以外，还存在一种特殊的类——抽象类。如果在类的定义中存在着一些抽象的方法，那么这种类就称为抽象类。语法上，抽象类是不能用于实例化对象的。
>
> 举个例子，中国人（`Chinese` 类）和美国人（`American` 类）都有“吃饭”这个行为，因此可以先定义一个 `Person` 类，然后让 `Chinese` 和 `American` 都继承这个类。但如何在父类 `Person` 中定义“吃饭”这个方法呢？一般而言，中国人是用筷子吃饭，并且吃的是中餐；而美国人是用刀叉吃饭，吃的是西餐，显然二者对于“吃饭”这一行为的具体实现是不同的。因此，无法在父类 `Person` 中具体的定义“吃饭”这一方法。此时，就可以将 `Person` 定义成一个抽象类，并将“吃饭”这个行为定义成抽象方法（只有方法声明，但没有方法体的方法），然后再在子类 `Chinese` 和 `American` 中分别对“吃饭”进行具体的实现。
>
> 可见，抽象类往往用来表示抽象概念。

在面向对象分析和设计的过程中，经过封装和继承的分析之后，可以先创建一个抽象的父类，该父类定义了其所有子类共享的一般形式（如 `Person` 类），具体细节再由子类来完成（如 `Chinese` 类和 `American` 类）。 Java 中定义抽象类的语法形式如下。

```java
abstract class 类名{ }
```

Java 也提供了一种特殊的方法，这个方法不是一个完整的方法，只含有方法的声明，没有方法体，这样的方法叫做抽象方法，其语法形式如下。

```java
访问修饰符 abstract 返回值 方法名( );
```

接下来通过一个例子来了解抽象类的使用。

现有 `Person` 类、`Chinese` 类和 `American` 类三个类，其中 `Person` 类为抽象类，含有 `eat()`和 `work()`两个抽象方法，其类关系如图所示。

![图片描述](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/8c8a77289aeae2b83a03fba704e64506-0)

首先在终端输入以下命令创建一个 `Test.java` 文件。

```bash
touch Test.java
```

`Person` 类的代码如下所示。

```java
//定义抽象类Person
abstract class Person {
    String name = "人";
    String color = "肤色";

    //定义吃饭的抽象方法eat()
    public abstract void eat();

    //定义工作的抽象方法eat()
    public abstract void work();
}
```

以上，在抽象类 `Person` 中定义了 `eat()`和 `work()`两个抽象方法。接下来，在子类 `Chinese` 和 `American` 中分别对这两个方法进行实现。 `Chinese` 类代码如下所示。

```java
//子类Chinese继承自抽象父类Person
class Chinese extends Person {

    //实现父类eat()的抽象方法
    public void eat() {
        System.out.println("中国人用筷子吃饭！");
    }

    //实现父类work()的抽象方法
    public void work() {
        System.out.println("中国人勤劳工作！");
    }
}
```

`American` 类代码如下所示。

```java
//子类American继承自抽象父类Person
class American extends Person {
    String belief = "基督教";            //信仰

    //实现父类eat()的抽象方法
    public void eat() {
        System.out.println("美国人用刀叉吃饭！");
    }

    //实现父类work()的抽象方法
    public void work() {
        System.out.println("美国人快乐工作！");
    }
}
```

可见，子类 `Chinese` 和 `American` 对抽象类 `Person` 中两个抽象方法的具体实现是不同的。

测试类代码如下所示。

```java
class TestAbstract {
    public static void main(String[] args) {
        Person liuHL = new Chinese();    //创建一个中国人对象
        System.out.println("***中国人的行为***");
        liuHL.eat();                    //调用中国人吃饭的方法
        liuHL.work();                //调用中国人工作的方法
        Person jacky = new American();    //创建一个美国人对象
        System.out.println("***美国人的行为***");
        jacky.eat();                    //调用美国人吃饭的方法
        jacky.work();                //调用美国人工作的方法
    }
}
```

综上所述，`Test.java` 文件完整代码如下所示。

```java
//定义抽象类Person
abstract class Person {
    String name = "人";
    String color = "肤色";

    //定义吃饭的抽象方法eat()
    public abstract void eat();

    //定义工作的抽象方法eat()
    public abstract void work();
}
//子类Chinese继承自抽象父类Person
class Chinese extends Person {

    //实现父类eat()的抽象方法
    public void eat() {
        System.out.println("中国人用筷子吃饭！");
    }

    //实现父类work()的抽象方法
    public void work() {
        System.out.println("中国人勤劳工作！");
    }
}
//子类American继承自抽象父类Person
class American extends Person {
    String belief = "基督教";            //信仰

    //实现父类eat()的抽象方法
    public void eat() {
        System.out.println("美国人用刀叉吃饭！");
    }

    //实现父类work()的抽象方法
    public void work() {
        System.out.println("美国人快乐工作！");
    }
}
class TestAbstract {
    public static void main(String[] args) {
        Person liuHL = new Chinese();    //创建一个中国人对象
        System.out.println("***中国人的行为***");
        liuHL.eat();                    //调用中国人吃饭的方法
        liuHL.work();                //调用中国人工作的方法
        Person jacky = new American();    //创建一个美国人对象
        System.out.println("***美国人的行为***");
        jacky.eat();                    //调用美国人吃饭的方法
        jacky.work();                //调用美国人工作的方法
    }
}
```

![image-20211127151834472](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127151834472.png)

在上面例子的基础上，进一步了解抽象类的语法特征。

**抽象类不能被直接实例化。**

抽象类中可以包含着抽象方法，而抽象方法是没有方法体的。因此如果将一个抽象类进行实例化，然后调用其中的抽象方法，会是一种无意义的方法调用。试想，`new Person().eat()`方法的运行结果有何意义？所以，为了避免这种无意义的方法调用，在语法上抽象类是不能被直接实例化的。

例如，在测试类代码中写如下的语句时，编译器就会报错，提示抽象类无法被实例化。

```java
Person liuHL = new Person();
```

**抽象类的子类必须实现抽象方法（除非这个子类也是抽象类）。**

抽象类是以父类的形式出现的，是对子类的规约，要求子类必须实现抽象父类的抽象方法。例如，抽象类 `Person` 就通过定义抽象方法的形式，规定了子类必须实现 `eat()`和 `work()`两个方法。如果将 `Chinese` 类的 `work` 方法变为注释，使抽象类中的抽象方法没有被子类实现，编译时就会报错。

**抽象类里可以有普通方法，也可以有抽象方法，但是有抽象方法的类必须是抽象类。**

去掉 `Person` 类前的 `abstract` 关键字，使 `Person` 类不再是抽象类，却含有抽象方法，编译时报错。

需要注意的是，抽象类里面也可以没有抽象方法，只是把原来的类前面加上 `abstract` 关键字，使其变为抽象类。例如，以下定义抽象类的代码是符合语法规范的。

```java
abstract class Person {
    //普通方法
    public void aMethod()
    { ... }
}
```

#### 2.接口

> 上一节详细介绍了抽象类，提到抽象类中可以有抽象方法，也可以有普通方法，但是有抽象方法的类必须是抽象类。与抽象类类似，但又与之不同的另一个概念是“接口”：如果一个“类”中的方法全部都是抽象方法，那么由这些抽象方法组成的特殊的“类”实际就是所说的接口，定义接口使用的关键字是 `interface`。

接口是一系列抽象方法的集合，与抽象类不同，不可以声明普通方法。

虽然有人常说，接口是一种特殊的抽象类，但是在面向对象编程的设计思想层面，两者还是有显著区别的。抽象类更侧重于对相似的类进行抽象，形成抽象的父类以供子类继承使用；而接口往往在程序设计的时候，定义模块与模块之间应满足的规约或者定义一种标准，使各模块之间能协调工作。

Java 接口定义的语法形式如下。

```java
[修饰符] interface 接口名 [extends] [接口列表]{ 接口体 }
```

interface 前的修饰符是可选的，如果使用修饰符，则只能用 public 修饰符，表示此接口是公有的，在任何地方都可以引用它，这一点和类是相同的。 接口是和类同一层次的，所以接口名的命名规则参考类名命名规则即可。

extends 关键词和类语法中的 extends 类似，用来定义直接的父接口。和类不同，一个接口可以继承多个父接口，当 extends 后面有多个父接口时，它们之间用逗号隔开。

接口体就是用大括号括起来的那部分，在接口体里定义接口的成员，包括常量和抽象方法。

类实现接口的语法形式如下：

```java
[修饰符] class 类名 implements 接口列表{ 类体 }
```

类实现接口用 `implements` 关键字，Java 中的类只能是单继承的，但一个 Java 类可以实现多个接口，这也是 Java 解决多继承的方法。

接下来通过一个实际的例子来说明接口的作用。

如今，蓝牙技术已经在社会生活中广泛应用。移动电话、蓝牙耳机、蓝牙鼠标、平板电脑等电子设备都支持蓝牙实现设备间短距离通信。那为什么这些不同的设备能通过蓝牙技术进行数据交换呢？其本质在于蓝牙提供了一组规范和标准，规定了频段、速率、传输方式等要求，各设备制造商按照蓝牙规范约定制造出来的设备，就可以按照约定的模式实现短距离通信。蓝牙提供的这组规范和标准，就是所谓的接口。 蓝牙接口创建和使用步骤如下。

- 各相关组织、厂商约定蓝牙接口标准。
- 相关设备制造商按约定接口标准制作蓝牙设备。
- 符合蓝牙接口标准的设备可以实现短距离通信。

下面通过代码来模拟蓝牙接口规范的创建和使用步骤。 首先在终端输入以下命令新建一个 `InterfaceTest` 文件夹，并自行修改文件目录为下图所示。

![图片描述](https://doc.shiyanlou.com/courses/3232/1533757/c641df7583768991670dd5d6a62aaacc-0)

接着定义蓝牙的接口标准。

假设蓝牙接口通过 `input()` 和 `output()` 两个方法提供服务，这时就需要在蓝牙接口中定义这两个抽象方法，在 `BlueTooth.java` 文件中输入以下代码。

```java
//定义蓝牙接口
public interface BlueTooth {
    //提供输入服务
    public void input();

    //提供输出服务
    public void output();
}
```

然后定义蓝牙耳机类，实现蓝牙接口，在 `Earphone.java` 文件中输入以下代码。

```java
public class Earphone implements BlueTooth {
    String name = "蓝牙耳机";

    //实现蓝牙耳机输入功能
    public void input() {
        System.out.println(name + "正在输入音频数据...");
    }

    //实现蓝牙耳机输出功能
    public void output() {
        System.out.println(name + "正在输出反馈信息...");
    }
}
```

再定义 `iPad` 类，实现蓝牙接口，在 `iPad.java` 文件中输入以下代码。

```java
public class iPad implements BlueTooth {
    String name = "iPad";

    //实现iPad输入功能
    public void input() {
        System.out.println(name + "正在输入数据...");
    }

    //实现iPad输出功能
    public void output() {
        System.out.println(name + "正在输出数据...");
    }
}
```

最后编写测试类，对蓝牙耳机类和 `iPad` 类进行测试，在 `TestInterface.java` 文件中输入以下代码。

```java
public class TestInterface {
    public static void main(String[] args) {
        BlueTooth ep = new Earphone();    //创建并实例化一个实现了蓝牙接口的蓝牙耳机对象ep
        ep.input();                    //调用ep的输入功能
        BlueTooth ip = new iPad();        //创建并实例化一个实现了蓝牙接口的iPad对象ip
        ip.input();                    //调用ip的输入功能
        ip.output();                    //调用ip的输出功能
    }
}
```

![image-20211127153506184](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127153506184.png)

再看另一个接口的例子。目前，电子邮件是人们广泛使用的一种信息沟通形式，要创建一封电子邮件，至少需要发信者邮箱、收信者邮箱、邮件主题和邮件内容 4 个部分。可以采用接口定义电子邮件的这些约定，让电子邮件类（实现类）必须实现这个接口，从而达到让电子邮件必须满足这些约定的要求。

定义电子邮件接口，在 `EmailInterface.java` 文件里面输入以下代码。

```java
public interface EmailInterface {
    //设置发信者邮箱
    public void setSendAdd(String add);

    //设置收信者邮箱
    public void setReceiveAdd(String add);

    //设置邮件主题
    public void setEmailTitle(String title);

    //设置邮件内容
    public void writeEmail(String email);
}
```

定义电子邮件类，实现 `EmailInterface` 接口，在 `Email.java` 中输入以下代码。 注意，在实现接口中抽象方法的同时，邮箱类本身还有一个 `showEmail()`方法。

```java
//定义Email，实现Email接口
public class Email implements EmailInterface {
    String sendAdd = "";            //发信者邮箱
    String receiveAdd = "";            //收信者邮箱
    String emailTitle = "";            //邮件主题
    String email = "";                //邮件内容

    //实现设置发信者邮箱
    public void setSendAdd(String add) {
        this.sendAdd = add;
    }

    //实现设置收信者邮箱
    public void setReceiveAdd(String add) {
        this.receiveAdd = add;
    }

    //实现设置邮件主题
    public void setEmailTitle(String title) {
        this.emailTitle = title;
    }

    //实现设置邮件内容
    public void writeEmail(String email) {
        this.email = email;
    }

    //显示邮件全部信息
    public void showEmail() {
        System.out.println("***显示电子邮件内容***");
        System.out.println("发信者邮箱：" + sendAdd);
        System.out.println("收信者邮箱：" + receiveAdd);
        System.out.println("邮件主题：" + emailTitle);
        System.out.println("邮件内容：" + email);
    }
}
```

定义一个邮件作者类。 邮件作者类中含静态方法 `writeEmail(EmailInterface email)`，用于写邮件，在 `EmailWriter.java` 中输入以下代码。

```java
import java.util.Scanner;
class EmailWriter {
    //定义写邮件的静态方法，形参是EmailInterface接口
    public static void writeEmail(EmailInterface email) {
        Scanner input = new Scanner(System.in);
        System.out.print("请输入发信者邮箱：");
        email.setSendAdd(input.next());
        System.out.print("请输入收信者邮箱：");
        email.setReceiveAdd(input.next());
        System.out.print("请输入邮件主题：");
        email.setEmailTitle(input.next());
        System.out.print("请输入邮件内容：");
        email.writeEmail(input.next());
//email.showEmail();//编译无法通过，因为形参email是EmailInterface接口，没有此方法
    }
}
```

编写测试类，在 `TestInterface2.java` 中输入以下代码。 测试类代码首先创建并实例化出一个实现了电子邮件接口的对象 `email`，然后调用 `EmailWriter` 类的静态方法 `writeEmail` 写邮件，最后将 `email` 对象强制类型转换成 `Email` 对象（不提倡此做法），调用 `Email` 类的 `showEmail()`方法。

```java
public class TestInterface2 {
    public static void main(String[] args) {
        //创建并实例化一个实现了电子邮件接口的对象email
        EmailInterface email = new Email();
        //调用EmailWriter类的静态方法writeEmail写邮件
        EmailWriter.writeEmail(email);
        //强制类型转换，调用Email类的showEmail()方法（不是接口方法）
        ((Email) email).showEmail();
    }
}
```

![image-20211127154809464](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127154809464.png)

接下来了解接口的语法特征。

**接口中不允许有实体方法。jkd8及以后可以有静态方法和默认方法**

例如，在 `EmailInterface` 接口中增加下面的实体方法。

```java
//显示邮件全部信息
public void showEmail(){
}
```

编译时就会报错，提示接口中不能有实体方法，

**接口中可以有成员变量，修饰符默认为 `public static final`（即便不写修饰符也默认是这样），因为是常量所以必须在声明时对这些成员变量赋初值。可以这样说，接口中的成员变量实际就是常量。接口中的抽象方法默认且必须是 `public` 的。**

在 `EmailInterface` 接口中，增加表示邮件发送端口号的成员变量 `sendPort`，代码如下。

```java
int sendPort = 25; // 等价于 public static final int sendPort = 25;
```

在 `Email` 类的 `showEmail()`方法中增加语句`System.out.println("发送端口号：" + sendPort);`，含义为访问 `EmailInterface` 接口中的 `sendPort` 并显示出来。

运行 `TestInterface2` 类，程序运行结果如图所示:

![image-20211127155549618](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127155549618.png)

**一个类可以实现多个接口。**

假设一个邮件，不仅需要符合 `EmailInterface` 接口对电子邮件规范的要求，而且需要符合对发送端和接收端端口号接口规范的要求，才允许成为一个合格的电子邮件。

在 `Interface` 文件夹里面新建一个 `PortInterface.java`,并输入以下代码。

```java
public interface PortInterface {
    // 设置发送端端口号
    public void setSendPort(int port);
    // 设置接受端端口号
    public void setReceivePort(int port);
}
```

`Email` 类不仅要实现 `EmailInterface` 接口，还要实现 `PortInterface` 接口，同时类方法中必须实现 `PortInterface` 接口的抽象方法。将 `Email.java` 替换成如下代码。

```java
    //定义 Email，实现 Email 接口
    public class Email implements EmailInterface {
    String sendAdd = ""; //发信者邮箱
    String receiveAdd = ""; //收信者邮箱
    String emailTitle = ""; //邮件主题
    String email = ""; //邮件内容

        int sendPort = 25;        //发送端端口号
        int receivePort = 110;     //接收端端口号

        //实现设置发送端端口号
        public void setSendPort(int port) {
            this.sendPort = port;
        }

        //实现设置接收端端口号
        public void setReceivePort(int port) {
            this.receivePort = port;
        }

        //实现设置发信者邮箱
        public void setSendAdd(String add) {
            this.sendAdd = add;
        }

        //实现设置收信者邮箱
        public void setReceiveAdd(String add) {
            this.receiveAdd = add;
        }

        //实现设置邮件主题
        public void setEmailTitle(String title) {
            this.emailTitle = title;
        }

        //实现设置邮件内容
        public void writeEmail(String email) {
            this.email = email;
        }

        //显示邮件全部信息
        //显示邮件全部信息
        public void showEmail() {
            System.out.println("***显示电子邮件内容***");
            System.out.println("发送端端口号：" + sendPort);
            System.out.println("接收端端口号：" + receivePort);
            System.out.println("发信者邮箱：" + sendAdd);
            System.out.println("收信者邮箱：" + receiveAdd);
            System.out.println("邮件主题：" + emailTitle);
            System.out.println("邮件内容：" + email);
        }

    }
```

![image-20211127160737302](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127160737302.png)

**接口可以继承其他接口，实现接口合并的功能。**

在刚才的代码中，让一个类（`Email`）实现了多个接口（`EmailInterface` 和 `PortInterface` 接口），但是再在 `EmailWriter` 类的 `writeEmail()`方法中传入对象时，形参就必须是这个类（`Email`），而不能是该类实现的某个接口。因为根据多态的知识，多态对象只能调用定义该对象的类和其父接口中的方法，因此如果给 `writeEmail()`方法设置的形参只是某一个接口（如 `EmailInterface` 接口）类型，那么该形参将无法调用其他接口（`PortInterface` 接口）中的方法。但如果将方法的参数类型设置为一个类而不是一个接口，这样做就不是我们推荐的面向接口编程了。接下来在刚才例子的基础上，用接口继承的方式解决这个问题。

将 `EmailInterface.java` 替换成如下代码。

```java
//让邮件接口继承 PortInterface 接口
public interface EmailInterface extends PortInterface {
//设置发信者邮箱
public void setSendAdd(String add);
//设置收信者邮箱
public void setReceiveAdd(String add);
//设置邮件主题
public void setEmailTitle(String title);
//设置邮件内容
public void writeEmail(String email);
}
```

`PortInterface` 接口、`Email` 类的代码不用调整，`EmailWriter` 类和测试类 `TestInterface3` 中 `writeEmail()`方法的参数类型改为 `EmailInterface` 接口，这样的程序就体现了面向接口编程的特性，可以实现多态性。`EmailWriter` 类和测试类 `TestInterface3` 中的代码分别如下。

```java
import java.util.Scanner;
class EmailWriter {
//定义写邮件的静态方法，形参是EmailInterface接口
public static void writeEmail(EmailInterface email) {
Scanner input = new Scanner(System.in);
System.out.print("请输入发信者邮箱：");
email.setSendAdd(input.next());
System.out.print("请输入收信者邮箱：");
email.setReceiveAdd(input.next());
System.out.print("请输入邮件主题：");
email.setEmailTitle(input.next());
System.out.print("请输入邮件内容：");
email.writeEmail(input.next());
//email.showEmail();//编译无法通过，因为形参email是EmailInterface接口，没有此方法
}
}
    public class TestInterface3 {
        public static void main(String[] args) {
            //创建并实例化一个实现了电子邮件接口的对象email
            EmailInterface email = new Email();
            //调用EmailWriter类的静态方法writeEmail写邮件
            EmailWriter.writeEmail(email);
            //强制类型转换，调用Email类的showEmail()方法（不是接口方法）
            ((Email) email).showEmail();
        }
    }
```

在终端输入如下命令运行此程序，结果如下图所示。

![image-20211127161010060](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127161010060.png)

在接口的应用中，有一个非常典型的案例，就是实现打印机系统的功能。在打印机系统中，有打印机对象，有墨盒对象（可以是黑白墨盒，也可以是彩色墨盒），有纸张对象（可以是 A4 纸，也可以是 B5 纸）。怎么才能让打印机、墨盒和纸张等生产厂商生产的不同设备组装在一起成为打印机进行正常打印呢？解决的办法就是接口。

打印机系统开发的主要步骤如下。

- 打印机和墨盒之间需要接口，定义为墨盒接口 PrintBox，打印机和纸张之间需要接口，定义为纸张接口 PrintPaper。
- 定义打印机类，引用墨盒接口 PrintBox 和纸张接口 PrintPaper，实现打印功能。
- 定义黑白墨盒和彩色墨盒实现墨盒接口 PrintBox，定义 A4 纸和 B5 纸实现纸张接口 PrintPaper。
- 编写打印系统，调用打印机实施打印功能。

首先输入以下命令新建一个 `Print` 文件夹

`PrintBox` 和 `PrintPaper` 接口的代码如下所示。

```java
//墨盒接口
public interface PrintBox {
    //得到墨盒颜色，返回值为墨盒颜色
    public String getColor();
}
//纸张接口
public interface PrintPaper {
    //得到纸张尺寸，返回值为纸张尺寸
    public String getSize();
}
```

打印机类 `Printer `的代码如下。

```java
//打印机类
public class Printer {
    //使用墨盒在纸张上打印
    public void print(PrintBox box, PrintPaper paper) {
        System.out.println("正在使用" + box.getColor() + "墨盒在" + paper.getSize() + "纸张上打印！");
    }
}
```

黑白墨盒类 `GrayPrintBox` 和彩色墨盒类 `ColorPrintBox` 的代码如下。

```java
//黑白墨盒，实现了墨盒接口
public class GrayPrintBox implements PrintBox {
    //实现getColor()方法，得到“黑白”
    public String getColor() {
        return "黑白";
    }
}
//彩色墨盒，实现了墨盒接口
public class ColorPrintBox implements PrintBox {
    //实现getColor()方法，得到“彩色”
    public String getColor() {
        return "彩色";
    }
}
```

A4 纸类 `A4Paper` 和 B5 纸类 `B5Paper` 的代码如下。

```java
//A4纸张，实现了纸张接口
public class A4Paper implements PrintPaper {
    //实现getSize()方法，得到“A4”
    public String getSize() {
        return "A4";
    }
}
//B5纸张，实现了纸张接口
public class B5Paper implements PrintPaper {
    //实现getSize()方法，得到“B5”
    public String getSize() {
        return "B5";
    }
}
```

在 `TestPrinter.java` 文件中输入以下代码进行测试。

```java
public class TestPrinter {
    public static void main(String[] args) {
        PrintBox box = null;            //墨盒
        PrintPaper paper = null;        //纸张
        Printer printer = new Printer();    //打印机
        //使用彩色墨盒在B5纸上打印
        box = new ColorPrintBox();
        paper = new B5Paper();
        printer.print(box, paper);
        //使用黑白墨盒在A4纸上打印
        box = new GrayPrintBox();
        paper = new A4Paper();
        printer.print(box, paper);
    }
}
```

![image-20211127162612824](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127162612824.png)

#### 3.内部类

#### 1.成员内部类

成员内部类 `InnerClass` 可以直接访问外部类 `OuterClass` 中的属性和方法，如下所示。

新建一个 `OuterClass.java` 文件，输入以下代码。

```java
public class OuterClass {
    //属性
    String name;

    //方法
    public void method() {
    }

    public static void staticMethod() {
    }

    //成员内部类
    class InnerClass {
        private String name= "张三";

        private void invokeOuter() {
            System.out.println(name);
            method();
            staticMethod();
        }
    }
}
```

对于成员内部类的使用，需要先生成外部类对象，然后再以 **外部类对象.new 内部类()** 的形式生成内部类对象，如下所示。

```java
public class OuterClass {
    ...

    public static void main(String[] args) {
        //定义外部类对象
        OuterClass outer = new OuterClass();
        //定义内部类对象
        InnerClass inner = outer.new InnerClass();
        inner.invokeOuter();
    }
}
```

程序运行结果如下。

![image-20211127163136014](C:\Users\Oxygen\AppData\Roaming\Typora\typora-user-images\image-20211127163136014.png)

#### 2.静态内部类

静态内部类 `InnerClass` 只能访问外部类 `OuterClass` 的静态属性和静态方法，如下所示。

新建一个 `OuterClass2.java` 文件，并输入以下代码。

```java
package 抽象类和接口;

public class OuterClass2 {
    private String age = "";
    private static String name = "李四";

    public void method() {};
    public static void staticMethod(){};
    static class InnerClass{
        private static String testStrInner = "";
        public static void testInner() {
            staticMethod();
            System.out.println(name);
        }
    }
    public static void main(String[] args) {
        InnerClass.testInner();
    }
}
```

静态成员可以通过类名直接调用，如 **类名.方法()**。与之类似，静态内部类中的方法也可以通过 **静态内部类名.方法()** 的形式调用

![image-20211127163652386](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127163652386.png)

如果测试类和静态内部类不在同一个`.java` 文件中，那么可以通过 **外部类名.静态内部类.方法()** 的形式调用。例如，如果将上述程序中的 `main()`移到其他类中，那么就可以通过`OuterClass2.InnerClass.testInner();`来调用静态内部类 `InnerClass` 中的 `testInner()`方法。

#### 3.局部内部类

JDK8.0 以后，局部内部类 `InnerClass` 在访问外部方法 `method()`定义的变量时，可以省略给变量加 final 修饰，如下所示。

新建一个 `OuterClass3.java` 文件，并输入以下代码。

```java
public class OuterClass3 {
    public static void method() {
        String name="Hello";
        class InnerClass {
            public void innerMethod() {
                System.out.println(name);
            }
        }
        // new InnerClass().innerMethod();
    }
}
```

局部内部类只能在定义它的方法内部使用，因此如果要调用局部内部类中定义的 `innerMethod()`方法，将上述程序中`new InnerClass().innerMethod() ;`前面的注释打开即可。局部内部类的定义，并不会影响外部类方法的使用，如下所示。

```java
public class OuterClass3 {
    ...
   public static void main(String[] args) {
        OuterClass3 outerClass = new OuterClass3();
        outerClass.method();
        OuterClass3.method();
    }
}
```

![image-20211127164503205](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127164503205.png)

#### 4.匿名内部类

假如有一个类，我们只用这个类创建一次对象，且对象只用一次。这样的话这个类的复用率就太低了，用匿名内部类可以很好的解决这个问题，如下所示：

```java
public class AnonymousInnerClass {
    public static void main(String[] args) {
        System.out.println(new AnonymousInnerClass().getClass());
        IA tiger = new IA() {
            @Override
            public void cry() {
                System.out.println("老虎叫唤！");
            }
        };
        tiger.cry();
        System.out.println(tiger.getClass().getName());   // 随机分配一个类名


        Outer01 inner = new Outer01() {
            public void clas() {
                System.out.println("Inner!!!!!!");
            }
        };
        inner.clas();
        Outer02 outer02 = new Outer02() {
            @Override
            void abs() {
                System.out.println("abs Inner");
            }
        };
        outer02.abs();
    }

}


interface IA {
    void cry();
}


class Outer01 {
    public void clas() {
    }
}


abstract class Outer02 {
    abstract void abs();
}
```

![image-20211204154022480](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211204154022480.png)





多线程对象是 Thread 类型的，启动线程的方法是 `start()`方法，并且线程的执行逻辑可以以 Runnable 参数的形式放在 Thread 的构造方法中，即`new Thread(Runnable 对象).start()`就可以启动一个线程。但 Runnable 是一个接口，其中包含了一个 `run()`抽象方法，如果用以前的做法，我们就需要先定义一个 Runnable 的实现类，然后再实现类中重写 `run()`方法，最后再创建一个 Runnable 实现类的对象，并把这个对象传入到 `Thread()`构造方法中。但显然这样做过于复杂，此时就可以通过匿名内部类的形式简化代码，如下所示。

```java
public class OuterClass4 {
    public static void main(String[] args) {
        new Thread((new Runnable() {
            @Override
            public void run() {
                // 多线程执行逻辑
                System.out.println("多线程..");
            }
        })).start();
    }
}
```

![image-20211127165014298](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211127165014298.png)

#### 5.小结

- 抽象类中既可以包含抽象方法，也可以包含普通方法；但如果一个类中存在抽象方法，那么该类一定是抽象类。
- 接口中只能存在常量和抽象方法；并且常量的修饰符是用 `static final` 修饰的，方法是用 `abstract` 修饰的。
- 抽象和接口往往用于自顶向下的设计程序。
- 接口和抽象类都不能用于实例化对象，但抽象类有构造方法，接口没有。
- 接口中的方法必须全部都是抽象方法，但抽象类中的方法既可以有抽象方法，也可以有普通方法。
- 对于类，Java 只支持单继承；但一个接口可以通过继承多个接口。
- 抽象类除了不能实例化对象之外，其它如成员变量、成员方法和构造方法的访问方式等仍然和普通类一样。
- 内部类是定义在类中的类，根据定义的类位置及修饰符的不同，分为了成员内部类，静态内部类，局部内部类、匿名内部类等四种类型。



### 11.枚举类

> 枚举是一组常量的集合。
>
> 枚举属于一种特殊的类，里面只包含一组有限的特定的对象。

枚举实现的两种方式：

1. 自定义类实现枚举。
2. 使用enum关键字实现枚举

#### 1.自定义类实现枚举

```java
package Enum;

import jdk.nashorn.internal.runtime.FindProperty;

/**
 * @author Zhtao
 * @date 2021/12/5 0:58
 */
public class Enumeration02 {
    public static void main(String[] args) {
        System.out.println(Season.SPRING);
    }
}

// 自定义枚举实现
class Season {
    private String name;
    private String desc;

    public final static Season SPRING = new Season("春天", "温暖");
    public final static Season WINTER = new Season("冬天", "寒冷");
    public final static Season SUMMER = new Season("夏天", "炎热");
    public final static Season AUTUMN = new Season("秋天", "凉爽");

    // 1.将构造器私有化，防止直接创建对象
    // 2.去掉seter方法，防止属性被修改
    // 3.在Season内部，直接创建固定的对象，
    // 4.优化，加入final修饰符
    public Season(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }


    public String getDesc() {
        return desc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }
}
```

#### 2. 使用enum关键字实现枚举类

```java
package Enum;

/**
 * @author Zhtao
 * @date 2021/12/5 1:08
 */
public class Enumeration03 {
    public static void main(String[] args) {
        System.out.println(Season.SPRING);
    }
}

// 使用enum关键字实现枚举类
enum Season2 {
    // 1.使用关键字enum代替class
    // 2.public final static Season SPRING = new Season("春天", "温暖");使用SPRING("春天", "温暖"),代替
    // 3.如果有多个常量(对象)用都好分隔。
    // 4.使用enum需要将定义常量对象放在最前面

    SPRING("春天", "温暖"), // 相当于调用构造器创建对象，只是简化了
    WINTER("冬天", "寒冷"),
    SUMMER("夏天", "炎热"),
    AUTUMN("秋天", "凉爽");
    private String name;
    private String desc;
	// 可以省略private关键字
    private Season2(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }


    public String getDesc() {
        return desc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }
}
```

- enum关键字注意事项:

  1. 当我们使用enum关键字创建一个枚举类时，默认会继承Enum类，而且是一个final类

     我们用javap命令反编译Season2：

     

![image-20211205135658923](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205135658923.png)

2. ​	如果使用无参构造器创建枚举对象，则实参列表和小括号可以省略。

   ```java
   AUTO,
   SPRING("春天", "温暖"),
   WINTER("冬天", "寒冷"),
   SUMMER("夏天", "炎热"),
   AUTUMN("秋天", "凉爽");
   private String name;
   private String desc;
   private Season2() {
   }
   ```

3. 构造器的修饰必须是private或者省略，只能是private且默认是private

#### 3.enum常用方法一览表

![image-20211205141008796](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205141008796.png)

```java
package Enum;

/**
 * @author Zhtao
 * @date 2021/12/5 14:10
 *  演示Enum类各种方法的使用
 */
public class EnumMethod {
    public static void main(String[] args) {
        Season2 autumn = Season2.AUTUMN;
        System.out.println(autumn.name());// 输出这个枚举对象的名称-AUTUMN
        System.out.println(autumn.ordinal());// 输出这个枚举对象的次序。春夏秋冬，从0开始编号
        // 从反编译可以看出，values方法，返回Season2[]，
        // 含有定义的所有枚举对象
        Season2[] values = Season2.values();
        // 循环遍历
        for (Season2 season2 :values) {
            System.out.println(season2);
        }
        // 到枚举对象中找AUTUMN，找到就返回，找不到就报错。
        Season2 autumn1 = Season2.valueOf("AUTUMN");
        System.out.println("autumn1="+autumn1);
        // compareTo比较两个枚举对象的编号。
        System.out.println(Season2.AUTUMN.compareTo(Season2.SPRING)); //2   Season2.AUTUMN.ordinal() - Season2.SPRING.ordinal
    }
}
```

![image-20211205143446045](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205143446045.png)

**练习**

```java
package Enum;

/**
 * @author Zhtao
 * @date 2021/12/5 14:26
 */
public class EnumExercise02 {
    public static void main(String[] args) {
        System.out.println("=====所有的星期信息如下=====");
        for (Week week : Week.values()) {
            System.out.println(week);
        }
    }
}

enum Week {
    MONDAY("星期一"), TUESDAY("星期二"), WEDNESDAY("星期三"), THURSDAY("星期四"), FRIDAY("星期五"), SATURDAY("星期六"), SUNDAY("星期日");
    private String name;

    private Week(String day) {
        this.name = day;
    }

    @Override
    public String toString() {
        return this.name;
    }
}
```

![image-20211205143531658](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205143531658.png)

**小结：**

1. 使用enum关键字后就不能再继承其他类了，因为用了enum关键字后，这个类已经继承了Enum类，而Java是单继承的。

2. 枚举类和其他类一样，可以实现接口。

   ```java
   enum 类名 implements 接口1,接口2{}
   ```

```java
package Enum;

/**
 * @author Zhtao
 * @date 2021/12/5 14:38
 */
public class EnumDetail {
    public static void main(String[] args) {
        Music.CLASSIMUSIC.playing();
    }
}

interface IPlaying {
    public void playing();
}

enum Music implements IPlaying {	// 实现接口
    CLASSIMUSIC;
    @Override
    public void playing() {
        System.out.println("正在播放音乐.....");
    }
}
```

### 12.JDK内置的注解

- @override：限定某个方法，是重写父类方法，该注解只能用于方法。
- @deprecated：用于表示某个程序元素（类，方法等）已过时。
- @suppresswarnings：印制编译器警告。

#### 1.@override

```java
class Father {
    public void fly() {
        System.out.println("Father fly");
    }
}

class Son extends Father {
    // 1. @Override放在fly方法上，表示重写父类fly方法。
    // 2. 不写@Override，还是重写了父类fly方法。
    // 3. 如果写了@override，编译器就会检查改方法是否重写了父类方法，如果的确重写了，编译通过，如果没有重写，编译报错。
    // 4. @Override的定义
    // @interface 表示一个注解类
    // @Target是修饰注解的注解，成为元注解。
    /*
        @Target(ElementType.METHOD)     // ElementType.METHOD说明这个注解只能放在方法上。
        @Retention(RetentionPolicy.SOURCE)
        public @interface Override {
        }
     */
    @Override 
    public void fly() {
        System.out.println("Son Fly");
    }
}
```

#### 2.@deprecated

```java
package annotation;

/**
 * @author Zhtao
 * @date 2021/12/5 15:04
 */
public class deprecated_ {
    public static void main(String[] args) {
        A a = new A();
        a.hi();
    }
}


// 1. @Deprecated修饰某个元素，表示某个元素已经过时。
// 2. 即不推荐使用，但仍然可以使用。
// 3. 查看源码
// 4. 可用于构造器、字段/属性、变量、方法、包、参数、类型。
// 5. @Deprecated可以用于版本升级过度使用
/*
    @Documented
    @Retention(RetentionPolicy.RUNTIME)
    @Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE})
    public @interface Deprecated {
    }
*/
@Deprecated
class A {
    private int n1 = 10;

    @Deprecated
    public void hi() {
        System.out.println("hi");
    }
}
```

![image-20211205164023320](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205164023320.png)

可以看到使用被@Deprecated注解的元素在使用时会有个删除线。

#### 3.suppresswarnings

```java
package annotation;

import java.util.ArrayList;
import java.util.List;

/**
 * @author Zhtao
 * @date 2021/12/5 16:44
 */
public class SuppressWarnings_ {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("jack");
        list.add("tom");
        list.add("mary");
        int i;
        System.out.println(list.get(1));
    }
}
```

![image-20211205164701770](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205164701770.png)

可以看到当前有些代码被黄色方块包裹着，这是一种警告。如果不希望看到这个警告，可以用suppresswarnings来印制警告。

![image-20211205165437430](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211205165437430.png)

| **关键字**               | **用途**                                                     |
| ------------------------ | ------------------------------------------------------------ |
| all                      | to suppress all warnings （抑制所有警告）                    |
| boxing                   | to suppress warnings relative to boxing/unboxing operations （抑制装箱、拆箱操作时候的警告） |
| cast                     | to suppress warnings relative to cast operations （抑制映射相关的警告） |
| dep-ann                  | to suppress warnings relative to deprecated annotation （抑制启用注释的警告） |
| deprecation              | to suppress warnings relative to deprecation （抑制过期方法警告） |
| fallthrough              | to suppress warnings relative to missing breaks in switch statements （抑制确在switch中缺失breaks的警告） |
| finally                  | to suppress warnings relative to finally block that don’t return （抑制finally模块没有返回的警告） |
| hiding                   | to suppress warnings relative to locals that hide variable（抑制相对于隐藏变量的局部变量的警告） |
| incomplete-switch        | to suppress warnings relative to missing entries in a switch statement (enum case)（忽略没有完整的switch语句） |
| nls                      | to suppress warnings relative to non-nls string literals（ 忽略非nls格式的字符） |
| null                     | to suppress warnings relative to null analysis（ 忽略对null的操作） |
| rawtypes                 | to suppress warnings relative to un-specific types when using generics on class params（ 使用generics时忽略没有指定相应的类型） |
| restriction              | to suppress warnings relative to usage of discouraged or forbidden references（ 抑制禁止使用劝阻或禁止引用的警告） |
| serial                   | to suppress warnings relative to missing serialVersionUID field for a serializable class（ 忽略在serializable类中没有声明serialVersionUID变量） |
| static-access            | to suppress warnings relative to incorrect static access（ 抑制不正确的静态访问方式警告） |
| synthetic-access         | to suppress warnings relative to unoptimized access from inner classes（ 抑制子类没有按最优方法访问内部类的警告） |
| unchecked                | to suppress warnings relative to unchecked operations（ 抑制没有进行类型检查操作的警告） |
| unqualified-field-access | to suppress warnings relative to field access unqualified（ 抑制没有权限访问的域的警告） |
| unused                   | to suppress warnings relative to unused code（ 抑制没被使用过的代码的警告） |

```java
package annotation;

import java.util.ArrayList;
import java.util.List;

/**
 * @author Zhtao
 * @date 2021/12/5 16:44
 */
public class SuppressWarnings_ {
    // 1. 当我们不想看到警告时，可以使用SuppressWarnings注解来印制警告。
    // 2.在{""}中填写想印制的警告类型。
    // 4.SuppressWarnings印制范围是跟放置的位置有关的
    // 比如放在main方法上面，印制的就是main方法中的元素
    // 5. 源码分析
    // (1)可以放在类、字段、方法、参数、构造器、局部变量
    // (2) 该注解类有数组String[] value()设置一个数组比如{"all"}
    /*
        @Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
        @Retention(RetentionPolicy.SOURCE)
        public @interface SuppressWarnings {
            String[] value();
        }
     */
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("jack");
        list.add("tom");
        list.add("mary");
        int i;
        System.out.println(list.get(1));
    }
}
```

#### 4.JDK元注解

> jdk的元Annotation用于修饰其他Annotation
>
> 元注解的种类：
>
> 1. Retention：指定注解的作用范围，三种SOURCE，CLASS，RUNTIME
> 2. Target：指定注解可以在那些地方使用
> 3. Documened：指定该注解是否会在javadoc体现
> 4. Inherited：子类会继承父类注解。

### 13.异常

> 概念：Java语言中，将程序执行中发生的不正常情况称为”异常“。（开发过程中的语法错误和逻辑错误不是异常）
>
> 执行过程中所发生的异常事件可分为两类
>
> 1. Error(错误)：Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重错误。比如StackOverflowError[栈溢出]和OOM(out of memory),Error是严重错误，程序会崩溃。
> 2. Exception：其他因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性代码进行处理。例如控制着访问，试图读取不存在的文件，网络链接中断等等，Exception分为两大类：运行时异常[]和编译时异常[]。

```java
package Exception_;

/**
 * @author Zhtao
 * @date 2021/12/7 18:03
 */
public class Exception01 {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 0;
        // 除数为0 报ArithmeticException算术异常
        int yes = num1 / num2;
        System.out.println("程序正在运行...");
    }
}
```

![image-20211207180828327](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207180828327.png)

#### 1.常见的运行时异常

- NullPointerException 空指针异常

  - 当应用程序在需要对象的地方使用null，抛出该异常

  ```java
  package Exception_;
  
  /**
   * @author Zhtao
   * @date 2021/12/7 21:48
   */
  public class NullPointerException_ {
      public static void main(String[] args) {
          String name = null;
          System.out.println(name.length());
      }
  }
  ```

  ![image-20211207214956967](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207214956967.png)

- ArithmeticException 数字运算异常

  - 当出现异常的运算条件时，抛出此异常，例如：一个整数”除以零“时抛出此异常。

  ```java
  package Exception_;
  
  /**
   * @author Zhtao
   * @date 2021/12/7 18:03
   */
  public class Exception01 {
      public static void main(String[] args) {
          int num1 = 10;
          int num2 = 0;
          // 除数为0 报ArithmeticException算术异常
          int yes = num1 / num2;
          System.out.println("程序正在运行...");
      }
  }
  ```

  ![image-20211207180828327](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207180828327.png)

- ArrayIndexOutOfBoundsException 数组下标越界异常

  - 用非法索引访问数组时抛出此异常，如果索引为负或大于等于数组的长度，则该索引为非法索引。

  ```java
  package Exception_;
  
  /**
   * @author Zhtao
   * @date 2021/12/7 21:53
   */
  public class ArrayIndexOutOfBoundsException_ {
      public static void main(String[] args) {
          int[] arr = {1,2,3};
          System.out.println(arr[3]);
      }
  }
  ```

  ![image-20211207215400754](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207215400754.png)

- ClassCastException 类型转换异常

  - 当试图将对象强制转换为不是实例的子类时，抛出该异常。

  ```java
  package Exception_;
  
  /**
   * @author Zhtao
   * @date 2021/12/7 21:55
   */
  public class ClassCastException_ {
      public static void main(String[] args) {
          A b = new B();  // 向上转型
          B b2 = (B)b;    // 向下转型
          C c = (C)b;
      }
  }
  
  
  class A {}
  class B extends A{}
  class C extends A{}
  ```

  ![image-20211207215916827](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207215916827.png)

- NumberFormatException 数字格式不正确异常[]

  - 当应用程序试图将字符串转换成一种数值时，但该字符不能转换为合适的格式时，抛出该异常 => 使用异常我们可以确保输入的是满足条件的数字。

  ```java
  package Exception_;
  
  /**
   * @author Zhtao
   * @date 2021/12/7 22:01
   */
  public class NumberFormatException_ {
      public static void main(String[] args) {
          String name = "1234";
          // 将字符串转换为整数
          int num = Integer.parseInt(name);
          System.out.println(num);    // 1234
          String name1 = "tom";
          // 将字符串转换为整数
          int num1 = Integer.parseInt(name1);
  
      }
  }
  ```

  ![image-20211207220344917](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211207220344917.png)

#### 2.编译异常

> 编译异常是指在编译期间，就必须处理的异常，否则代码不能通过编译。

- SQLException：操作数据库时，查询表可能发生异常。
- IOException：操作文件时，发生的异常
- FileNotFoundException：当操作一个步卒年在的文件时，发生异常
- ClassNotFoundException：加载类，而该类不存在时，发生异常
- EOFException：操作文件，到文件末尾，发生异常
- IllegalArguementException：参数异常。

#### 3.异常处理

> 当异常发生时，对异常进行处理。

- 异常处理的方式：

  - try-catch-finally

    程序员在代码中捕获发生的异常，自行处理。

  - throms

    将发生的异常抛出，交给调用者（方法）处理，最顶级的处理者是JVM。

**try-catch-finally语法：**

```java
try {
    // 代码/可能有问题的代码
} catch (Exception e) {
    // 捕获到的异常
    // 1.当异常发生时
    // 2.系统将异常封装成Exception对象e，传递给catch
    // 3.的到异常对象后，程序员自己处理。

} finally {
    // 不管是否发生异常，总会执行的代码。
}
```

**throms语法：**

```java
public class Throws_ {
//    public void f1() throws FileNotFoundException,NullPointerException {
    public void f1() throws Exception {
        // 创建了一个文件流对象
        // FileNotFoundException异常，编译异常
        // 使用throws，抛出异常，让调用f1()方法的调用者处理
        // throws 关键字后也可以是 异常列表，即可以抛出多个异常。
        FileInputStream f1 = new FileInputStream(".");
    }
}
```

**自定义异常：**

> 当程序中出现了某些"错误"，但是该错误信息并没有在Throwable子类中描述处理，这个时候可以自己设计异常类，用于描述该错误信息。

- 自定义异常的步骤
  1. 定义类：自定义异常类名（程序员自己写）继承Exception或RuntimeException
  2. 如果继承Exception，属于编译异常
  3. 如果继承RuntimeException，属于运行异常（一般来说，继承RuntimeException）

我们自定义一个年龄范围在18-120范围内的异常类：

```java
package Throws_;

/**
 * @author Zhtao
 * @date 2021/12/8 19:57
 */
public class CustomException {
    public static void main(String[] args) {
        int age = 180;
        // 要求age的范围在18-120之间，否则抛出异常。
        if (!(age>=18 && age<=120)) {
            throw new AgeException("年龄需要在18-120之间!");
        }
    }
}


// 自定义异常
// 1. 一般自定义异常都是继承RuntimeException
// 2. 把自定义异常做成运行异常，好处是：我们可以使用默认的处理机制
// 3. 比较方便
class AgeException extends RuntimeException {
    public AgeException(String message) {
        super(message);
    }
}
```

![image-20211208200511180](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211208200511180.png)

当age的值小于18或大于120时，就会抛出异常。

**throw和throws区别:**

|        | 意义                     | 位置       | 后面跟东西 |
| ------ | ------------------------ | ---------- | ---------- |
| throws | 异常处理的一种方式       | 方法声明中 | 异常类型   |
| throw  | 手动生成异常对象的关键字 | 方法体中   | 异常对象   |

测试题：

```java
package Throws_;

/**
 * @author Zhtao
 * @date 2021/12/8 20:11
 */
public class ReturnExceptionDemo {
    static void methodA() {
        try {
            System.out.println("进入方法A");
            throw new RuntimeException("制造异常");
        } finally {
            System.out.println("用A方法的finally");
        }
    }
    static void methodB() {
        try {
            System.out.println("进入方法B");
        } finally {
            System.out.println("调用B方法的finally");
        }
    }

    public static void main(String[] args) {
        try {
            ReturnExceptionDemo.methodA();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
        ReturnExceptionDemo.methodB();
    }
}
```

![image-20211208202342075](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211208202342075.png)

### 14.常用类

#### 1.装箱和拆箱

> 装箱：基本类型=> 包装类型
>
> 拆箱：包装类型=> 基本类型

1. jdk5前的手动装箱和拆箱方式

2. jdk5及以后的自动装箱拆箱方式

3. 自动装箱地城调用的是valueOf方法，比如Integer.valueOf()

```java
package wrapper;

/**
 * int 和Integer装箱和拆箱
 * @author Zhtao
 * @date 2021/12/9 22:06
 */
public class Integer01 {
    public static void main(String[] args) {
        // jdk5以前手动装箱
        int n1 = 100;
        Integer integer = new Integer(n1);
        Integer integer1 = Integer.valueOf(n1);
        // jdk5以前手动拆箱
        int i = integer.intValue();
        // jdk5及后自动装箱与拆箱
        int n2 = 100;
        Integer integer2 = n2; // 底层使用的是Integer.valueOf(n2);
        // 自动拆箱
        int n3 = integer2;  // 底层使用的是integer.intValue();
    }
}
```

#### 2.Integer和String的互相转换

```java
package wrapper;

/**
 * Integer和String类型互相转换
 * @author Zhtao
 * @date 2021/12/9 22:16
 */
public class WrapperVSString {
    public static void main(String[] args) {
        // Integer=>String
        Integer n = 100;
        // 方式1
        String str1 = n + "";
        System.out.println(str1);
        // 方式2
        String str2 = n.toString();
        // 方式3
        String str3 = String.valueOf(n);

        // String => Integer
        String str4 = "1234";
        // 方式1
        Integer n2 = Integer.parseInt(str4);    // Integer.parseInt(str4);返回类型是int，然后自动装箱
        // 方式2
        Integer n3 = new Integer(str4);
    }
}
```

#### 4.Integer和Character的常用方法

```java
package wrapper;

import java.sql.SQLOutput;

/**
 * @author Zhtao
 * @date 2021/12/9 22:25
 */
public class IntegerAndCharacter_ {
    public static void main(String[] args) {
        System.out.println(Integer.MAX_VALUE);  // 最大值
        System.out.println(Integer.MIN_VALUE);  // 最小值
        System.out.println(Character.isDigit('a')); // 判断是不是数字
        System.out.println(Character.isLetter('a'));    // 判断是不是字幕
        System.out.println(Character.isUpperCase('a')); // 判断是不是大写
        System.out.println(Character.isLowerCase('a')); // 判断是不是小写
        System.out.println(Character.isWhitespace('a'));    // 判断是不是空格
        System.out.println(Character.toUpperCase('a')); // 转成大写
        System.out.println(Character.toLowerCase('A')); // 转成小写
    }
}
```

#### 5.String结构

1. String对象用于保存字符串，也就是一组字符序列

2. ”jack“字符串常量，双引号括起来的字符序列

3. 字符串的字符使用Unicode字符编码，一个字符(不区分字母还是汉字)占两个字节

4. String类有很多构造器，构造器的重载

   常用的有 String s1 = new String();

   String s2 = new String(String original);

   String s3 = new String(Char[] a);

   String s4 = new String(char[] a,int startIndex,int count);

   String s5 = new String(Byte[] b)

5. String类实现了接口Serializable(String可以串行化：可以在网络传输)

   
