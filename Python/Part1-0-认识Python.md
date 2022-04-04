
## 认识Python

### Python的介绍
Python（英国发音：/ˈpaɪθən/ 美国发音：/ˈpaɪθɑːn/）是一种广泛使用的解释型、高级和通用的编程语言。Python支持多种编程范型，包括函数式、指令式、结构化、面向对象和反射式编程。它拥有动态类型系统和垃圾回收功能，能够自动管理内存使用，并且其本身拥有一个巨大而广泛的标准库。

Python是开源编程语言，可以在各种领域中用于编写独立的程序和脚本。Python免费、可移植、功能强大，而且使用起来相当容易。

#### Python的发展历程

1. 1989年圣诞节：Guido von Rossum开始写Python语言的编译器。
2. 1991年2月：第一个Python编译器（同时也是解释器）诞生，它是用C语言实现的，可以调用C语言的库函数。在该版本中，Python已经存在了带继承的类、异常处理、函数和核心数据类型list、dict、str等。
3. 1994年1月：Python 1.0正式发布。主要新特征是包括了Amrit Prem提供的函数式编程工具lambda、map、filter和reduce。
4. 2000年10月16日：Python 2.0发布，增加了实现完整的垃圾回收，提供了对Unicode的支持。
5. 2008年12月3日：Python 3.0发布，它并不完全兼容之前的Python代码，不过因为目前还有不少公司在项目和运维中使用Python 2.x版本，所以Python 3.x的很多新特性后来也被移植到Python 2.6/2.7版本中。

目前我们使用的Python 3.7.x的版本是在2018年发布的，Python的版本号分为三段，形如A.B.C。其中A表示大版本号，一般当整体重写，或出现不向后兼容的改变时，增加A；B表示功能更新，出现新功能时增加B；C表示小的改动（例如：修复了某个Bug），只要有修改就增加C。

#### Python适用的领域

Python在Web应用开发、云基础设施、DevOps、网络爬虫开发、数据分析挖掘、机器学习等领域都有着广泛的应用，因此也产生了Web后端开发、数据接口开发、自动化运维、自动化测试、科学计算和可视化、数据分析、量化交易、机器人开发、图像识别和处理等一系列的职位。

### Python环境的搭建

在[Python官方网站](<https://www.python.org>)可以下载所需的安装程序。

#### Python的安装


### Python开发工具介绍

#### IDLE - 自带的集成开发工具

IDLE是安装Python环境时自带的集成开发工具。

#### IPython - 交互式编程工具
> IPython是一种基于Python的交互式解释器。可以通过Python的包管理工具pip安装IPython和Jupyter。

```Shell
pip install ipython
```
或

```Shell
pip3 install ipython
```

> Jupyter工具并运行名为notebook的程序在浏览器窗口中进行交互式代码编写操作。

```Shell
pip install jupyter
```

或

```Shell
pip3 intall jupyter
```

然后执行下面的命令：

```Shell
jupyter notebook
```

#### PyCharm - Python开发工具

PyCharm是由JetBrains公司开发的提供给Python专业的开发者的一个集成开发环境，它最大的优点是能够大大提升Python开发者的工作效率，为开发者集成了很多用起来非常顺手的功能，包括代码调试、高亮语法、代码跳转、智能提示、自动补全、单元测试、版本控制等等。

### 练习：第一个Python：Hello World！

```python

print "hello world！"

```
