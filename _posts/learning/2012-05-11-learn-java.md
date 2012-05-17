---
layout: post
title: "Thinking in Java"
category: learning
tags: [java]
description: |
  java的经典名著，第一次惧于他的厚度，现在回过头来看看也感觉受益匪浅，java是我喜欢的语言之一，正如他的名字一样优雅。
---
{% include JB/setup %}

##第1章 对象导论

面向对象的三要素：封装、继承、多态。

封装是将事物抽象为类，隐藏具体实现。命令式语言是对汇编语言的抽象，汇编是对底层机器的抽象，面向对象语言是对所解决问题的抽象。


两种方法使基类和导出类产生差异：子类添加新方法、子类复写父类中的方法。

在处理类型的层次结构时，把对象当做基类的对象来处理，这样代码就能脱离具体类型。面向对象函数调用采用后期绑定，相对象发送消息时，被调用的代码直到运行时才能知道调用方法的绝对地址，编译器只确保方法存在和类型检查。后期绑定即动态绑定，这是实现多态的前提。面向基类编程的过程称为向上转型，多态可以使事物总是被正确的处理。

单根继承性：java所有的类都继承自单一的基类Object，单根继承性使得所有的对象都可以执行一些基本的操作。

向上转型是安全的，参数化类型，即泛型消除了向下转型的犯错误的可能。

对象数据的两种存储方式：堆栈（stack）和堆（heap）。C++的对象数据存放在堆栈中，这样得到了最大的执行速度，丧失了灵活性，对象的存储空间和生命周期都在程序编写时确定。java对象数据在堆内存池中动态创建，垃圾回收机制在对象不被使用时自动销毁，释放内存。

原始的web服务（服务器—浏览器）是一个简单的单项过程，即客户端向服务器发出一个请求，服务器返回一个文件，客户端解读文件。html只提供简单的 数据收集的作用，数据提交通过CGI（common gateway interface）传递 。客户端变成合理利用了客户机的资源，客户端编程的方法：插件、脚本语言。

applet提供了一中软件分发的方法，最终由于微软的封杀，被人遗忘。Flex以及Silverlight是一种applet的备选方案。Silverlight只局限于windows平台。移动平台似乎不喜欢插件，由于苹果的封杀，Flash穷头陌路。但是存在于98%的web浏览器上的Flash player，还有整个Adobe的多媒体生态环境的支撑，Flex短时间内还将是一个不错的富客户端解决方案。插件比脚本语言的优点在于开发者在编程时无需考虑浏览器的相关性。但是浏览器无插化是个趋势，html5、CSS3和javascript的完美结合将会是移动和PC平台web前段统一的解决方案。

##第2章 一切都是对象

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

##第3章 操作符

不可忽略的**赋值语句**：基本数据类型的赋值分配了新的存储空间，因为基本类型存储的是实际的数值；对一个对象的操作实际上是对对象引用的操作，因此对象的赋值只相当于给对象起了一个别名。将一个对象传递给方法，实际上传递的是一个引用，就如同C/C++中的变量名前加`&`，改变的是方法之外的对象。

C++和java中的**随机数**生成：C++中用`rand()`生成随机数，其实是伪随机数，因为它默认种子为1，不接收参数，每次产生的随机数序列是一样的，要传递种子产生随机数用`srand()`，常用当前时间作为种子，即`srand(time(0))`；java刚好相反，提供了一个产生随机数的类`Random`，而默认就是以当前时间为种子的，要是想产生相同的随机数序列，可以指定固定的种子。
{% highlight java linenos %}
import static java.lang.System.out;
import java.util.*;
public class Rand{
     public static void main(String[] args){
          Random rand=new Random(3);
          for(int i=0; i<10; i++){
               //产生1~100之间的随机数
               out.println((rand.nextInt(100)+1)+"\t");
          }
          for(int i=0; i<10; i++){
               //nextFloat产生float类型的随机数
               out.println(rand.nextFloat()+"\t");
          }
     }
}
{% endhighlight %}

自增自减的规律：前缀先生成值，后缀后生成值。
测试对象等价性的问题，关系操作符`==`和`!=`用于基本数据类型时比较的值得大小，用于对象时比较的是对象的引用，要比较对象的值用`equals()`，但是不适合基本类型。实际上默认的`equals()`方法（它是Object的方法）并不能比较两个对象的值，只是大多数的类都重写了该方法，猜一下下边程序的结果：
{% highlight java linenos %}
int a=1;int b=1;
out.println(a==b);
Integer aa=new Integer(1);
Integer bb=new Integer(1);
out.println(aa==bb);
out.println(aa.equals(bb));
aa=bb;
out.println(aa==bb);
Value va=new Value();
Value vb=new Value();
va.v=vb.v=1;
out.println(va.equals(vb));
out.println(va.v==vb.v);
{% endhighlight %}

如果你猜的没错，那结果应该是`true, false, true, true, false, true`。

直接常量后面的后缀字符（`l, f, d`及大写）标志了它的类型，java整数默认只支持十进制、十六进制（`0x, 0X`）、八进制（`0`），不能直接表示二进制，但是任意整数都可以使用`Integer.toBinaryString()`来显示二进制结果。

java的移位操作：
{% highlight java linenos %}
int s=8;
out.println(s<<2);
 int t=-8;
out.println(t>>2);
int r=-8;r>>>=2;     //无符号右移，高位插0
out.println(r);
{% endhighlight %}

值得注意的一点，对于布尔值按位操作符于逻辑操作符效果是一样的，只是按位操作符不会短路，逐位取反操作`~`只对符号位也起作用，如 `~1 = -2`，想得到期望的结果，可以`~(-1)`。

##第4章 控制执行流

java中不允许数字代表布尔值。java中唯一用到逗号操作符的是在for循环的控制表达式中，使用逗号操作符时，可以在for语句中定义多个变量，或执行多条步进语句，但是必须有相同的类型。

`return, continue, break`：return作用范围最大，可以跳出当前方法；普通的continue和break只能跳出当前循环；带标签的continue和break可以跳到标签位置。java中唯一需要用标签的地方就是嵌套循环。switch使用限制较多，选择因子只能是int或char这样的整数值，case后的break是可选的，但是会执行直到遇到break为止，default后的break是多余的。
{% highlight java linenos %}
//! 错误用法 out.println(True+4);
out.println((int)2.9);
out.println(Integer.MAX_VALUE+1);
//!if(1) out.println("1");
//逗号操作符
Random random=new Random();
for(int j=0, rand=0; ; rand=random.nextInt(10), out.println(rand), j++)
     if(rand>7)
          break;
int array[]={1,2,3,4,5,6,7,8,9,10};
for(int rand: array){
     out.print(rand+"\t");
}
//无穷循环
while(true){
     double rand=Math.random();
     out.println(rand);
     if(rand>0.9)
          break;
}
//标签及跳转
int i=0;
outer:
for(;;){
     inner:
     for(; i<10; i++){
          out.print(i+"\t");
          if(i==2) {out.println("continue"); continue;}
          if(i==3) {out.println("break"); i++; break;}
          if(i==7) {out.println("continue inner"); continue inner;}
          if(i==8) {out.println("break outer"); break outer;}
     }
}
label:
for(i=97;;i++){
     char ch=(char)i;
     switch(ch){
          case 'a': 
          case 'e':
          case 'm': out.print("m\t"); break;
          case 'n': out.print("n");
          case 'p': out.print("p"); break;
          case 'z': out.print("end"); break label;
          default: out.print("*\t");
     }
}
{% endhighlight %}

##第5章 初始化与清理

###构造器&初始化
在java中**初始化**和**创建**是捆绑在一起的，但是概念上将他们是彼此独立的。构造器没有返回值，这与返回值为空（void）不同。创建对象时实际上是返回一个对象的引用，而同时自动调用了构造器，如果构造器有返回值，就会与创建对象时返回的对象引用冲突，因为这两个过程是捆绑在一起的，没有办法分离，我想这就是构造器没有返回值的原因。

方法重载可以通过参数裂变来区分不同的方法，甚至参数顺序的不同也能区别两个方法，返回值的不同不能区分方法，因为忽略返回值的情况下会产生歧义。涉及基本类型的重载中，如果传入的方法类型小于声明中的方法类型，实际的数据类型会被提升（char可以提升为int），相反的过程不能通过编译。

自己创建构造器（无论有参无参），编译器都不会自动创建构造器。

this关键字表示对当前对象的引用，只能在内部使用，this可以用在返回当前的对象、将当前对象传递给其它方法、以及在构造其中调用构造器。使用this调用构造器需要注意：

- 使用this只能调用一个构造器，这是因为创建一个对象时也只能调用一个构造器来初始化，当然这个构造器可以自己实现，或者再调用其他构造器。
- 构造器调用必须放在起始位置，否则编译报错。
- 构造器只能是自动调用，或者由构造器调用，普通方法不能调用构造器，因为对象创建的生命周期中，构造方法只能调用一次，而普通方法只有在对象创建以后才能调用，而这时构造方法已经调用过了，就不能再调用。
{% highlight java linenos %}
import static java.lang.System.out;
import java.util.*;

class Person{
     public void eat(Apple apple){
          Apple peeled=apple.getPeeled();
          out.println(peeled.getState());
          out.println("yummy!");
     }
}
class Peeler{
     static Apple peel(Apple apple){
          apple.setState();
          return apple;
     }
}
class Apple{
     private String state="unpeel";
     public Apple getPeeled(){
          return Peeler.peel(this);
     }
     public void setState(){
          this.state="peeled";
     }
     public String getState(){
          return this.state;
     }
}
public class Test{
     public static void main(String[] args){
          class Leaf{
               Leaf(){};
               Leaf(int j){
                    out.println("get an int: "+j);
               }
               Leaf(String s){
                    out.println("get a String: "+s);
               }
               Leaf(int j, String s){
                    this(j);
                    //!this(s);
                    out.println("get a String: "+s);
               }
               int j=0;
               Leaf increment(){
                    j++;
                    return this;
               }
               void print(){
                    out.println("j= "+j);
               }
          }
          Leaf la=new Leaf();
          la.increment().increment().increment().print();
          Leaf lea=new Leaf(3, "leaf");
         
          new Person().eat(new Apple());    
     }
}
{% endhighlight %}

###终极处理&垃圾回收

java的垃圾回收器只会释放由new分配的内存，特殊的内存释放（如java中调用其他语言的代码），可以使用默认的`finalize()`函数（继承自Object），垃圾回收器回收动作发生时首先调用`finalize()`方法。

与 Java 不同，C++ 支持局部对象（基于栈）和全局对象（基于堆）。因为这一双重支持，C++ 提供了自动构造和析构，这导致了对构造函数和析构函数的调用，（对于堆对象）就是内存的分配和释放。在 Java 中，所有对象都驻留在堆内存，不存在局部对象，因此不需要析构来销毁局部对象。`finalize()`不同于C++的析构函数，JVM不一定会调用它，所以是不可靠的。使用`System.gc()`可以触发运行垃圾回收器，垃圾回收器会努力回收垃圾释放内存，但这并不意味着一定会执行`finalize()`。

java垃圾回收机制的策略是：程序濒临存储空间用完的时刻，垃圾回收器才会执行以释放内存，如果直到程序执行结束垃圾回收器也没有释放内存，那么随着程序的退出，内存会自动释放，交给操作系统。

使用`finalize()`的例子:
{% highlight java linenos %}
class Book{
     boolean checkedout=false;
     Book(boolean checkout){
          checkedout=checkout;
     }
     void checkin(){
          checkedout=false;
     }
     protected void finalize(){
          if(checkedout){
               out.println("Error: checked out!");
          }
     }
}
Book novel=new Book(true);
novel.checkin();
//Book boo=new Book(true);
//boo.finalize();
new Book(true);
//如果不使用匿名对象，System.gc()不一定触发finalize()，
//因为垃圾回收器不确定对象是否“存活”
System.gc();
{% endhighlight %}

###垃圾回收器的工作原理

垃圾回收器有效地提高了对象的创建速度，因为GC运行时一边释放内存，一边使堆中的对象存储更紧密，对对象进行重新排列，提高存取速度（“堆指针”跟接近地址入口）。

java的自适应垃圾回收技术：JVM进行监视，如果所有对象都很稳定，垃圾回收器的效率降低的话，就切换到**标记-清扫**方式；同样，JVM跟踪**标记-清扫**的效果，要是堆内出现很多碎片，就会切换回**停止-复制**方式。

###初始化

java尽力保证所有变量在使用前都初始化，对于局部变量未初始化的调用会产生编译错误。类的成员变量在对象创建时会得到一个默认的初始值（0或null），而且初始化的顺序是按照定义的顺序，即使是变量定义在调用方法之后，任然会先初始化变量。、

静态数据会默认得到一个初始化（如果没有对它进行初始化），需要注意的是`static`关键字不能用在局部变量。静态数据变量也能被修改，但只能是静态的修改。
{% highlight java linenos %}
class Spoon{
     static int i;
     static { i=47; }
     //!i=47;
}
{% endhighlight %}

非静态实例初始化时可以有静态初始化一样的语法，只不过没有static关键字，而且实例化是在构造器之前执行。

###可变参数列表

在参数个数类型未知的情况下创建一Object数组为参数的方法，这得益于java的单根继承性。
{% highlight java linenos %}
class VarArgs{
     static void printArray(Object[] arg){
          for(Object ar: arg)
               out.print(ar+"\t");
          out.println();
     }
}

public class Test{
     public static void main(String[] args){
          VarArgs.printArray(new Object[]{1, 2, 'a', "spam", new Date()});
          //!VarArgs.printArray();
     }
}
{% endhighlight %}
这种方法也有不便之处，就是得遵循数组的语法，Java SE5以后加入了更好的语法，同样的功能，上边的代码可以这么写（而且对以上的语法是兼容的）：
{% highlight java linenos %}
class VarArgsNew{
     static void printArray(Object...arg){
          for(Object obj: arg)
               out.println(obj+":"+obj.getClass());
     }
     static void printArrayString(int req, String...arg){
          //!out.println((req+1)+":"+req.getClass());
          out.println((req+1)+":");
          for(Object obj: arg)
               out.println(obj+":"+obj.getClass());
     }
}

public class Test{
     public static void main(String[] args){
          VarArgsNew.printArray(1, new Integer(2), 'a', "spam", new Date());
          VarArgsNew.printArray(1, new Integer(2), 'a', "spam", new Date());
          //还可以传递空值
          VarArgsNew.printArray();
          //可以限制传入类型
         VarArgsNew.printArrayString(1, "spam", new Date().toString());
     }
}
{% endhighlight %}

参照结果可以发现，在单一混合类型的参数列表中，自动包装机制有选择的的将基本类型提升为它的包装类，而在有明确类型要求的参数列表中，则不会。

###枚举类型

枚举可以看做一个特殊的类，它也有自己的方法（`ordinal(), static values()`）等，enum与switch语句可以很好的组合，扩展switch的一些功能：
{% highlight java linenos %}
enum Fruit{
     APPLE, ORANGE, PEAR
}
class EatFruit{
     Fruit fruit;
     EatFruit(Fruit fruit){
          this.fruit=fruit;
     }
     public void eat(){
          out.print("eating ");
          switch(fruit){
               case APPLE: out.println(fruit.APPLE); break;
               case ORANGE: out.println(fruit.ORANGE); break;
               case PEAR: out.println(fruit.PEAR); break;
               default: out.println("no eating");
          }
     }
}

public class Test{
     public static void main(String[] args){
          EatFruit 
          eta=new EatFruit(Fruit.APPLE),
          eto=new EatFruit(Fruit.ORANGE),
          etp=new EatFruit(Fruit.PEAR);
          eta.eat();
          eto.eat();
          etp.eat();
     }
}
{% endhighlight %}

##第6章 访问权限控制

<div class="alert alert-block alert-warn form-inline" style="text-align:center; vertical-align:middle; font-size: 16px; font-weight:300;">To be continue!</div>