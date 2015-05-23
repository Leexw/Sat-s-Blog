Python得学一学，是个很有用的工具。
网上寻找教程，有这么几个网站可以关注下：

-	[w3cschool](http://www.w3cschool.cc/python/python-tutorial.html)
-	[python.org](http://python.org)
-	[python中文教程](http://www.pythondoc.com)

#####疑惑
lambda的使用

#####W3cschool

**基础特点**

-	可能含有中文编码问题，如果发生无法输出中文编码，则需要在文件中加入“ # -*- coding: UTF-8 -*- 或者 #coding=utf-8”就好了
-	可以有三种执行方式：交互式，通过Python解释器的交互模式，在终端输入代码执行；脚本式，调用解释器执行脚本；可执行文件式，给脚本添加解释器路径（#!/usr/bin/python），可直接执行脚本
-	标识符区分大小写，通过下划线（_或者__）来标明特殊标识符
-	通过行缩进来控制代码段
-	通过新行来作为语句的结束符，可通过“\”来拼接两个语句
-	通过单引号（'）、双引号（""）、三引号（"""）来表示字符串，其中三引号可表示有换行的字符串
-	井号（#）用来注释
-	空行不是语法，但也是代码的一部分，用来分隔代码段，方便维护
-	raw_input()可用来给用户输入，并在按下回车之后退出程序
-	可在同一行中使用多条语句，并用分号（;）来分隔
-	有五种标准数据类型：Number、String、List、Tuple、Dictionary。
-	Number支持四种数值类型，Int、Long、Float、Complex。
-	可使用［头下标：尾下标］来获取子字符串，其中可用（＋）来拼接字符串，另外（*）是重复操作符号
-	可使用内置的函数进行数据类型的转换，如float（x）
-	**，指数运算符。//，取商的整数。<>等价于!= 。and 、or 、not为逻辑运算符。 in 、not in为成员运算符。is 、is not 身份运算符。
-	优先级，身份运算符>成员运算符>逻辑运算符。
-	0或者null为false，其他为true。
-	不支持switch，可使用多个elif来实现
-	可在同一行使用if ＋ 语句，if a＝＝b：print ”a==b”
-	支持while、for循环，支持break、continue、pass控制语句
-	通过使用len（）＋range（）可以将for in变成for（;;）的效果
-	在字符串前添加“r/R”表示原始字符串，添加“u”表示unicode字符
-	内嵌的字符串操作函数很强大
-	del是删除语句，可通过del删除列表中的元素
-	tuple元祖是不能修改的
-	处理时间和日期，可以使用time和calendar模块。
-	通过time.time（）可获取当前时间戳，通过time.localtime(time.time())可将时间戳转为时间元祖，通过time.asctime(time.time())可转为格式化后的时间。
-	函数格式，def functionname( parameters ):return [expression]，以def开始，以return结束。所有参数都是引用传递，支持必备参数、命名参数、缺省参数和不定长参数。
-	lambda格式，lambda [arg1 [,arg2...arg]]:expression，有自己的名字空间，不能访问之外的自有参数列表之外的参数。
-	默认变量都是局部变量，如果函数内使用的是全局变量，则可以加global关键词
-	三种导入模式：import、from import、from import * 。
-	input()可输出python表达式，File对象方法提供了操作文件的一系列方法，是内嵌的，OS对象方法提供了处理文件及目录的一系列方法，是在os模块里提供的。
-	可使用try except else来处理异常，也可以使用try finally添加不同的处理。通过raise抛出异常。

*Python中的关键字*
![](http://7xitbl.com1.z0.glb.clouddn.com/Screen Shot 2015-05-17 at 12.24.27 PM.png)

**进阶特点**

-	面向对象。Swift简直就是抄了很多Python的特性，初始化方式等。Python是垃圾回收机制，内存管理也是通过引用技术来实现，垃圾回收会销毁计数为0和循环引用的对象。使用双下划线"__"来表明私有变量或私有方法。
-	re模块使得Python具备了全部的正则表达式功能。有三个常用的处理函数match、search、sub
-	可以使用Python脚本进行CGI编程
-	Python支持很多种数据库，对应的数据库模块，可支持增删查改
-	Python的smtplib模块支持SMTP协议发送邮件
-	Python通过thread和threading两个模块进行多线程编程，同时在thread和threading中提供了锁，Queue模块提供了队列来实现数据同步。
-	可通过GUI库来进行界面开发
