---
layout: post
title: "Thinking in Java 学习笔记"
category: learning
tags: [learn, java]
description: |
  java的经典名著，第一次惧于他的厚度，现在回过头来看看也感觉受益匪浅，java是我喜欢的语言之一，正如他的名字一样优雅。
---
{% include JB/setup %}

##第一章 对象导论

面向对象的三要素：封装、继承、多态。

封装是将事物抽象为类，隐藏具体实现。命令式语言是对汇编语言的抽象，汇编是对底层机器的抽象，面向对象语言是对所解决问题的抽象。


两种方法使基类和导出类产生差异：子类添加新方法、子类复写父类中的方法。

在处理类型的层次结构时，把对象当做基类的对象来处理，这样代码就能脱离具体类型。面向对象函数调用采用后期绑定，相对象发送消息时，被调用的代码直到运行时才能知道调用方法的绝对地址，编译器只确保方法存在和类型检查。后期绑定即动态绑定，这是实现多态的前提。面向基类编程的过程称为向上转型，多态可以使事物总是被正确的处理。

单根继承性：java所有的类都继承自单一的基类Object，单根继承性使得所有的对象都可以执行一些基本的操作。

向上转型是安全的，参数化类型，即泛型消除了向下转型的犯错误的可能。

对象数据的两种存储方式：堆栈（stack）和堆（heap）。C++的对象数据存放在堆栈中，这样得到了最大的执行速度，丧失了灵活性，对象的存储空间和生命周期都在程序编写时确定。java对象数据在堆内存池中动态创建，垃圾回收机制在对象不被使用时自动销毁，释放内存。

原始的web服务（服务器—浏览器）是一个简单的单项过程，即客户端向服务器发出一个请求，服务器返回一个文件，客户端解读文件。html只提供简单的 数据收集的作用，数据提交通过CGI（common gateway interface）传递 。客户端变成合理利用了客户机的资源，客户端编程的方法：插件、脚本语言。

applet提供了一中软件分发的方法，最终由于微软的封杀，被人遗忘。Flex以及Silverlight是一种applet的备选方案。Silverlight只局限于windows平台。移动平台似乎不喜欢插件，由于苹果的封杀，Flash穷头陌路。但是存在于98%的web浏览器上的Flash player，还有整个Adobe的多媒体生态环境的支撑，Flex短时间内还将是一个不错的富客户端解决方案。插件比脚本语言的优点在于开发者在编程时无需考虑浏览器的相关性。但是浏览器无插化是个趋势，html5、CSS3和javascript的完美结合将会是移动和PC平台web前段统一的解决方案。

##第二章 一切都是对象

java对象操作的方式是引用。

数据存储方式：

1. 寄存器，速度最快，不能直接控制，按需分配，C/C++可以向编译器建议寄存器分配方式。
2. 堆栈，位于通用RAM（随机访问存储器），速度仅次于寄存器，但是要使用它，程序创建时系统必须知道存储在堆栈中的所有项的确切生命周期，这限制了程序的灵活性，所以java只将对象的引用和基本类型信息存放在堆栈中，这也是鼓励使用基本类型的原因。
3. 堆，通用的内存池（也位于RAM），用于存放java的所有对象数据，不同于堆栈的是，new一个对象后，当程序执行时才在堆中进行存储分配，当然这种灵活性的代价是用堆存储分配和清理要比堆栈消耗的时间多。
4. 常量存储，常量值通常直接存放在程序代码内部，由于他们不会被改变，所以是安全的。有时嵌入式系统中分离的常量也存放在ROM（只读存储器）中。
5. 非RAM存储，数据也可以完全存活于程序之外，这样可以相对独立于程序，例如流对象和持久化对象。在流对象中对象转化成字节流发送到其他机器。在持久化对象中，对象被存放在磁盘上，这种存储方式的好处是对象存放在其他媒介上，在需要时可以恢复，例如JDBC、Hibernate。

当申明一个事物是static时，这个域或方法不与对象实例相关联。通过类可以直接调用static方法或域，一个static字段对每个类来说只有一份存储空间，非static字段每个对象对应一份存储空间。static方法在对象未创建前可以调用（main()方法）。

javadoc的命令都只能在“/**”注释出现时，同样结束于“*/”。
一个例子：
{% highlight java %}
/** 计算阶乘。
* 执行方法为 java Factorial [param]
* @author Calvin
* @author www.mceiba.com
*/
public class Factorial{
     /** 主函数
     * @param args 计算阶乘的参数
     */
     public static void main(String[] args){
          int input=Integer.parseInt(args[0]);
          //int input=4;
          double result=factorial(input);
          System.out.println(result);
     }
     /** 函数体 */
     public static double factorial(int x){
          if(x<0)
               return 0.0;
          double fact=1.0;
          while(x>1){
               fact=fact*x;
               x-=1;
          }
          return fact;
     }
}
{% endhighlight %}

需要注意一点的是中文情况下使用javadoc命令需要设置字符集：
{% highlight java %}
javadoc -encoding UTF-8 -charset UTF-8  Factorial.java
{% endhighlight %}


<div class="alert alert-block alert-warn form-inline" style="text-align:center; vertical-align:middle; font-size: 16px; font-weight:300;">To be continue!</div>