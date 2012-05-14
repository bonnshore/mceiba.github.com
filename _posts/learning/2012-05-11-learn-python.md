---
layout: post
title: "Learning Python"
category: learning
tags: [python]
description: |
  因为图像处理的一些需要接触了python，一开始就被它的优雅、简洁所吸引，简单的使用过一段时间以后才理解，python评价很高不是没有道理的。
---
{% include JB/setup %}

##第一部分 使用入门

###第1章 问答环节

####选择python的原因：

- 软件质量，具有脚本语言便于编写的优点，同时可读性强，以及对OOP的支持使他优于shell、perl等脚本语言，而且功能更强大。
- 开发效率高，python是比C/C++、java更高级的语言，他语法更简洁，使人们可以更加专注于需要解决的问题，而不是拘泥于编程语言本身。
- 可移植性强，如果说C/C++是一处编写处处编译，java是一处编译处处运行，那么python就是一处编写处处运行。
- 标准库的支持，python有许多内置标准扩以及第三方库，我选择python做图像处理很重要的原因就是<code>Python+NumPy+OpenCV</code>的组合比Matlab便于移植和工程应用，同时又比C/C++更易于编写，而且还免费。此外，python在第三方的支持下可以进行网站开发（Django）、数值计算（SciPy、NumPy）、游戏开发（PyOpenGL）、应用软件开发（PyQt、wxPython）等各个方面。
- 组件集成，原始的Python就是用C实现的，所以很容易实现和C/C++的相互调用。在Jython和IronPython的逐渐成熟，python和java以及.Net等框架之间的通信变得异常简单，所以python他不是一个人在战斗。
- 享受乐趣，python的简洁高效使得编程称为一种乐趣。

此外，python还有诸多的优点足够吸引你，比如python支持面向对象，却又不像java一样强制使用面向对象，这就意味着你可以像C一样去用它解决一些简单的注重于过程的问题，同时又可以像C++、java一样运用面向对象的方式解决一些大型的工程问题；python区别于其他语言最明显的标志就是使用缩进而不是<code>{ }</code>来区分代码块，这也是很多人觉得python优雅的地方。

####关于脚本语言

很多人一提到脚本语言，第一感觉是干不了大事的语言，其实随着诸如python、ruby、javascript等一些脚本语言的迅速蹿红，这种观念很明显以及站不住脚了。维基百科对脚本语言的定义是“为了缩短传统的编写-编译-链接-运行（edit-compile-link-run）过程而创建的计算机编程语言”。python可以被认定是一种脚本语言，但是这取决于你要解决的问题，一般意义上讲，“脚本语言”更适合于描述python所支持的快速灵活的开发模式，而不是特定的应用领域。事实上，“脚本语言”和“程序语言”也是可以相互替代的，就像python超出了一般脚本语言的功能，而javascript也可以用来进行服务器端编程（Node.js）。

当然python也是有他固有的缺点的，可能执行速度慢慢是最重要的一条吧，python不能像C语言一样编译成底层的二进制代码（比如Intel芯片指令），而是转换成一种字节码的形式，之后再将字节码解释。不过速度慢的缺点也不是致命的，在硬件条件高速发展的今天，再加上云计算、虚拟化、超级计算机、分布式等技术的助力，计算机硬件环境已经提升到一个前所未有的高度，运算速度和程序员的解放之间的博弈似乎变得越来越明朗。

###第2章 Python如何运行程序

####解释器

解释器是代码与机器的计算机硬件之间的软件逻辑层。python的解释器主要完成字节码编译和程序执行：

- 字节码编译。程序执行时，解释器会将源代码编译成字节码，编译是简单的翻译过程，字节码是底层的、与平台无关的。字节码可以提高执行速度，但任然赶不上二进制码的执行速度，python编译过的字节码文件是以“.pyc”为后缀的，程序执行过后会存在于py文件同一目录下（如果程序对系统没有写入权，字节码将会生产于内存当中，程序执行结束时被简单的丢弃），程序未修改时，解释器会自动加载上次编译过的pyc文件，否则重新编译，当然单独的pyc文件也是可以被直接调用的。
- Python虚拟机（PVM）。编译后的字节码发送到PVM上执行，PVM是一个迭代运行指令的大循环，一个接一个的执行指令。

通过py2exe、PyInstaller、freeze等第三方工具，python可以生成真正的二进制文件，如windows下的exe文件。

###第3章 如何运行程序

python程序文件称之为模块，是python最大的程序结构，一个模块文件是一个独立的命名空间。Linux小的<code>#!/usr/local/bin/python</code>或<code>#!/usr/bin/env python</code>是为了指定脚本的执行程序。

导入操作只会执行一次，重新导入需要reload。

import和from的区别：import是将模块的整体导入，而from增加了额外的赋值操作，调用属性不用模块名称，但是from打破了命名空间的完备性，导入后程序中相同的变量会被覆盖。

<code>exec(open('spam.py').read())</code>相当于在调用的地方复制了模块，同样也会覆盖相同的变量名。

##第二部分 类型和运算

###第4章 介绍Python对象类型

python程序可以分解为模块、语句、表达式以及对象：

1. 程序由模块构成。
2. 模块包含语句。
3. 语句包含表达式。
4. 表达式建立并处理对象。

使用C/C++时很大的一部分工作都花费在用基本的数据类型和数据结构去构建表现层的组件，需要考虑内存分配、垃圾回收等乏味的工作，而且这是背离程序的真真目标的。python提供的强大的内置对象解决了这一问题，而且鼓励更多的使用内置对象，而不是自己实现的对象。

python的核心数据类型（内置对象）：数字、字符串、列表、字典、元组、文件、集合、其他类型（类型、None、布尔型）、编程单元类型（函数、模块、类）、与实现相关的类型（编译的代码堆栈跟踪）。

python中没有类型声明，运行的表达式的的语法决定了创建和使用对象的类型，一旦对象创建，就和对应的操作集合绑定了。python是动态类型（不需要声明，而是自动跟踪类型），同时也是强类型语言。

####数字

计算结果为全精度，相当于repr，print函数（在3.0以前为语句）可以打印出比较友好的结果，相当于str。

常用的数学工具包：math、random，以及第三方的NumPy等。

####字符串

字符串是单个字符的字符串的序列，可以进行下标、切片操作。但是字符串具有不可变性，即创建以后不能更改，不能对某一位置进行赋值。字符串除了一般序列的操作，还具有字符串特有的一些操作，如`find, replace, splite, upper, isalpha, restrip`等。此外还有一个格式化的高级操作：
{% highlight python %}
>>> '%s, eggs, and %s' % ('spam', 'SPAM!')
'spam, eggs, and SPAM!'
>>> '{0}, eggs, and {1}'.format('spam', 'SPAM!')
'spam, eggs, and SPAM!'
{% endhighlight %}

在python基本类型中，数字、字符串和元组是不可变的，列表和字典是可变的。

可用于多种类型的通用型操作都是以内置函数或者表达式的形式出现的（如`len(X), X[0]`），类型特定的操作一般是以方法调用的形式出现的（如`aString.upper()`）。

使用`dir`和`help`，可以获取对象的帮助信息，dir能给出所有的方法名，help函数可以获取方法的帮助信息。

三个单引号或双引号中可以包含多行字符，以r开头的字符串可以表示原始（raw）字符串常量（去掉反斜杠转义机制）：
{% highlight python %}
>>> msg='''aaaaaaaa
bbbbbbbb
cccccccc'''
>>> msg
'aaaaaaaa\nbbbbbbbb\ncccccccc'
>>> print(msg)
aaaaaaaa
bbbbbbbb
cccccccc
>>> r'C:\Program Files\ython'
'C:\\Program Files\\ython'
>>> r'C:\Program Files\Python'
'C:\\Program Files\\Python'
>>> R=r'C:\Program Files\Python'
>>> print(R)
C:\Program Files\Python
{% endhighlight %}

使用`re`模块可以支持正则表达式：
{% highlight python %}
>>> import re
>>> match=re.match('/(.*)/(.*)/(.*)', '/usr/home/spam')
>>> match.groups()
('usr', 'home', 'spam')
{% endhighlight %}

####列表

列表是任意对象的有序集合，没有固定大小，可以嵌套，可以改变，以及索引、切片等序列操作。类型特定的常用操作有：`append, pop, del, insert, remove, sort, reverse`等，这些方法都是直接对列表进行了改变。

列表递推式：
{% highlight python %}
>>> [i*10 for i in range(10) if i%2==0]
[0, 20, 40, 60, 80]
>>> [ord(x) for x in 'spam']
[115, 112, 97, 109]
{% endhighlight %}

解析语法创建生成器：
{% highlight python %}
>>> M=[[1,2,3],[4,5,6],[7,8,9]]
>>> G=(sum(row) for row in M)
>>> next(G)
6
>>> next(G)
15
{% endhighlight %}

####字典

字典是一种`key-value`型的映射，同样具有可变性，而且还支持边界以外的赋值，这与列表不同。
字典的常用操作有：映射、重放嵌套、键排序、if测试：
{% highlight python %}
>>> rec={'name': {'first': 'Bob', 'last': 'Smith'}, 'job': ['dev', 'mgr'], 'age': 40}
>>> rec
{'age': 40, 'job': ['dev', 'mgr'], 'name': {'last': 'Smith', 'first': 'Bob'}}
>>> rec['name']
{'last': 'Smith', 'first': 'Bob'}
>>> rec['job'].append('janitor')
>>> rec
{'age': 40, 'job': ['dev', 'mgr', 'janitor'], 'name': {'last': 'Smith', 'first': 'Bob'}}
>>> D={'a': 1, 'b': 2, 'c': 3}
>>> D
{'a': 1, 'c': 3, 'b': 2}
>>> Ks=list(D.keys())
>>> Ks
['a', 'c', 'b']
>>> Ks.sort()
>>> Ks
['a', 'b', 'c']
>>> for key in Ks:
     print(key, '=>', D[key])

     
('a', '=>', 1)
('b', '=>', 2)
('c', '=>', 3)
>>> 'e' in D
False
>>> value=D.get('x', 0)
>>> value
0
>>> value=D['b'] if 'b' in D else 0
>>> value
2
{% endhighlight %}

列表解析相关的函数如map和filter，通常运行得比for循环快。

####元组

元组类似于一个不可改变的列表，支持任意类型、任意嵌套以及常见的序列操作。元组提供了一种完整性的约束条件。

####文件

{% highlight python %}
#基本文件操作
f=open(r'C:\Users\Calvin\vim\python\somefile.txt','w')
f.write('name: Calvin\n')
f.write('email: zhangsp@163.com\n')
f.write('tel: 13893819438\n')
f.close()
#文件模式默认为'r'，只读打开时可以忽略
text=open(r'C:\Users\Calvin\vim\python\somefile.txt').read()
print text
#使用fileinput
import fileinput
for line in fileinput.input(r'C:\Users\Calvin\vim\python\somefile.txt'):
     print line
#使用urllib
from urllib import urlopen
text=urlopen('file:C:\\Users\\Calvin\\vim\python\\somefile.txt')
print(text.read().split())
{% endhighlight %}

####集合

集合是唯一不可变的对象的无序集合（列表是有序的），支持一般的数学集合操作。
{% highlight python %}
>>> X=set('spam')
>>> Y={'m','o','n','t','y'}
>>> X,Y
(set(['a', 'p', 's', 'm']), set(['y', 'm', 't', 'o', 'n']))
>>> X&Y
set(['m'])
>>> X|Y
set(['a', 'm', 'o', 'n', 'p', 's', 't', 'y'])
>>> X-Y
set(['a', 'p', 's'])
{% endhighlight %}

检查对象类型的方法：
{% highlight python %}
>>> L=[1,2,3]
>>> if type(L)==type([]): print('YES')

YES
>>> if type(L)==list: print('YES')

YES
>>> if isinstance(L, list): print('YES')

YES
{% endhighlight %}

###第5章 数字


<div class="alert alert-block alert-warn form-inline" style="text-align:center; vertical-align:middle; font-size: 16px; font-weight:300;">To be continue!</div>
