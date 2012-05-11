---
layout: post
title: "Learning Python 学习笔记"
category: learning
tags: [learn, python]
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


<div class="alert alert-block alert-warn form-inline" style="text-align:center; vertical-align:middle; font-size: 16px; font-weight:300;">To be continue!</div>
