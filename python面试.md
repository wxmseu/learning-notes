<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**


   * [Python语言特性](#python语言特性)
      * [1 Python的函数参数传递](#1-python的函数参数传递)
      * [2 Python中的元类(metaclass)](#2-python中的元类metaclass)
      * [3 @staticmethod和@classmethod](#3-staticmethod和classmethod)
      * [4 类变量和实例变量](#4-类变量和实例变量)
      * [5 Python自省](#5-python自省)
      * [6 字典推导式](#6-字典推导式)
      * [7 Python中单下划线和双下划线](#7-python中单下划线和双下划线)
      * [8 字符串格式化:\x和.format](#8-字符串格式化和format)
      * [9 迭代器和生成器](#9-迭代器和生成器)
      * [10 *args and <code>**kwargs</code>](#10-args-and-kwargs)
      * [11 面向切面编程AOP和装饰器](#11-面向切面编程aop和装饰器)
      * [12 鸭子类型](#12-鸭子类型)
      * [13 Python中重载](#13-python中重载)
      * [14 新式类和旧式类](#14-新式类和旧式类)
      * [15 __new__和<code>__init__</code>的区别](#15-__new__和__init__的区别)
      * [16 单例模式](#16-单例模式)
         * [1 使用__new__方法](#1-使用__new__方法)
         * [2 共享属性](#2-共享属性)
         * [3 装饰器版本](#3-装饰器版本)
         * [4 import方法](#4-import方法)
      * [17 Python中的作用域](#17-python中的作用域)
      * [18 GIL线程全局锁](#18-gil线程全局锁)
      * [19 协程](#19-协程)
      * [20 闭包](#20-闭包)
      * [21 lambda函数](#21-lambda函数)
      * [22 Python函数式编程](#22-python函数式编程)
      * [23 Python里的拷贝](#23-python里的拷贝)
      * [24 Python垃圾回收机制](#24-python垃圾回收机制)
         * [1 引用计数](#1-引用计数)
         * [2 标记-清除机制](#2-标记-清除机制)
         * [3 分代技术](#3-分代技术)
      * [25 Python的List](#25-python的list)
      * [26 Python的is](#26-python的is)
      * [27 read,readline和readlines](#27-readreadline和readlines)
      * [28 Python2和3的区别](#28-python2和3的区别)
      * [29 super init](#29-super-init)
      * [30 range and xrange](#30-range-and-xrange)
   * [操作系统](#操作系统)
      * [1 select,poll和epoll](#1-selectpoll和epoll)
      * [2 调度算法](#2-调度算法)
      * [3 死锁](#3-死锁)
      * [4 程序编译与链接](#4-程序编译与链接)
         * [1 预处理](#1-预处理)
         * [2 编译](#2-编译)
         * [3 汇编](#3-汇编)
         * [4 链接](#4-链接)
      * [5 静态链接和动态链接](#5-静态链接和动态链接)
      * [6 虚拟内存技术](#6-虚拟内存技术)
      * [7 分页和分段](#7-分页和分段)
         * [分页与分段的主要区别](#分页与分段的主要区别)
      * [8 页面置换算法](#8-页面置换算法)
      * [9 边沿触发和水平触发](#9-边沿触发和水平触发)
   * [数据库](#数据库)
      * [1 事务](#1-事务)
      * [2 数据库索引](#2-数据库索引)
      * [3 Redis原理](#3-redis原理)
         * [Redis是什么？](#redis是什么)
         * [Redis数据库](#redis数据库)
         * [Redis缺点](#redis缺点)
      * [4 乐观锁和悲观锁](#4-乐观锁和悲观锁)
      * [5 MVCC](#5-mvcc)
         * [<a href="http://lib.csdn.net/base/mysql">MySQL</a>的innodb引擎是如何实现MVCC的](#mysql的innodb引擎是如何实现mvcc的)
      * [6 MyISAM和InnoDB](#6-myisam和innodb)
   * [网络](#网络)
      * [1 三次握手](#1-三次握手)
      * [2 四次挥手](#2-四次挥手)
      * [3 ARP协议](#3-arp协议)
      * [4 urllib和urllib2的区别](#4-urllib和urllib2的区别)
      * [5 Post和Get](#5-post和get)
      * [6 Cookie和Session](#6-cookie和session)
      * [7 apache和nginx的区别](#7-apache和nginx的区别)
      * [8 网站用户密码保存](#8-网站用户密码保存)
      * [9 HTTP和HTTPS](#9-http和https)
      * [10 XSRF和XSS](#10-xsrf和xss)
      * [11 幂等 Idempotence](#11-幂等-idempotence)
      * [12 RESTful架构(SOAP,RPC)](#12-restful架构soaprpc)
      * [13 SOAP](#13-soap)
      * [14 RPC](#14-rpc)
      * [15 CGI和WSGI](#15-cgi和wsgi)
      * [16 中间人攻击](#16-中间人攻击)
      * [17 c10k问题](#17-c10k问题)
      * [18 socket](#18-socket)
      * [19 浏览器缓存](#19-浏览器缓存)
      * [20 HTTP1.0和HTTP1.1](#20-http10和http11)
      * [21 Ajax](#21-ajax)
   * [*NIX](#nix)
      * [unix进程间通信方式(IPC)](#unix进程间通信方式ipc)
   * [数据结构](#数据结构)
      * [1 红黑树](#1-红黑树)
   * [编程题](#编程题)
      * [1 台阶问题/斐波那契](#1-台阶问题斐波那契)
      * [2 变态台阶问题](#2-变态台阶问题)
      * [3 矩形覆盖](#3-矩形覆盖)
      * [4 杨氏矩阵查找](#4-杨氏矩阵查找)
      * [5 去除列表中的重复元素](#5-去除列表中的重复元素)
      * [6 链表成对调换](#6-链表成对调换)
      * [7 创建字典的方法](#7-创建字典的方法)
         * [1 直接创建](#1-直接创建)
         * [2 工厂方法](#2-工厂方法)
         * [3 fromkeys()方法](#3-fromkeys方法)
      * [8 合并两个有序列表](#8-合并两个有序列表)
      * [9 交叉链表求交点](#9-交叉链表求交点)
      * [10 二分查找](#10-二分查找)
      * [11 快排](#11-快排)
      * [12 找零问题](#12-找零问题)
      * [13 广度遍历和深度遍历二叉树](#13-广度遍历和深度遍历二叉树)
      * [17 前中后序遍历](#17-前中后序遍历)
      * [18 求最大树深](#18-求最大树深)
      * [19 求两棵树是否相同](#19-求两棵树是否相同)
      * [20 前序中序求后序](#20-前序中序求后序)
      * [21 单链表逆置](#21-单链表逆置)
      * [22 两个字符串是否是变位词](#22-两个字符串是否是变位词)
      * [23 动态规划问题](#23-动态规划问题)

<!-- markdown-toc end -->





# Python语言特性

## 1 Python的函数参数传递

看两个例子:

```python
a = 1
def fun(a):
    a = 2
fun(a)
print a  # 1
```

```python
a = []
def fun(a):
    a.append(1)
fun(a)
print a  # [1]
```

所有的变量都可以理解是内存中一个对象的“引用”，或者，也可以看似c中void*的感觉。

通过`id`来看引用`a`的内存地址可以比较理解：

```python
a = 1
def fun(a):
    print "func_in",id(a)   # func_in 41322472
    a = 2
    print "re-point",id(a), id(2)   # re-point 41322448 41322448
print "func_out",id(a), id(1)  # func_out 41322472 41322472
fun(a)
print a  # 1
```

注：具体的值在不同电脑上运行时可能不同。

可以看到，在执行完`a = 2`之后，`a`引用中保存的值，即内存地址发生变化，由原来`1`对象的所在的地址变成了`2`这个实体对象的内存地址。

而第2个例子`a`引用保存的内存值就不会发生变化：

```python
a = []
def fun(a):
    print "func_in",id(a)  # func_in 53629256
    a.append(1)
print "func_out",id(a)     # func_out 53629256
fun(a)
print a  # [1]
```

这里记住的是类型是属于对象的，而不是变量。而对象有两种,“可更改”（mutable）与“不可更改”（immutable）对象。在python中，strings, tuples, 和numbers是不可更改的对象，而 list, dict, set 等则是可以修改的对象。(这就是这个问题的重点)

当一个引用传递给函数的时候,函数自动复制一份引用,这个函数里的引用和外边的引用没有半毛关系了.所以第一个例子里函数把引用指向了一个不可变对象,当函数返回的时候,外面的引用没半毛感觉.而第二个例子就不一样了,函数内的引用指向的是可变对象,对它的操作就和定位了指针地址一样,在内存里进行修改。

如果还不明白的话,这里有更好的解释: http://stackoverflow.com/questions/986006/how-do-i-pass-a-variable-by-reference

## 2 Python中的元类(metaclass)

这个非常的不常用,但是像ORM这种复杂的结构还是会需要的,详情请看:http://stackoverflow.com/questions/100003/what-is-a-metaclass-in-python

## 3 @staticmethod和@classmethod

Python其实有3个方法，即静态方法(staticmethod)，类方法(classmethod)和实例方法,如下：

```python
def foo(x):
    print "executing foo(%s)"%(x)

class A(object):
    def foo(self,x):
        print "executing foo(%s,%s)"%(self,x)

    @classmethod
    def class_foo(cls,x):
        print "executing class_foo(%s,%s)"%(cls,x)

    @staticmethod
    def static_foo(x):
        print "executing static_foo(%s)"%x

a=A()

```

这里先理解下函数参数里面的self和cls.这个self和cls是对类或者实例的绑定,对于一般的函数来说我们可以这么调用`foo(x)`,这个函数就是最常用的,它的工作跟任何东西(类,实例)无关.对于实例方法,我们知道在类里每次定义方法的时候都需要绑定这个实例,就是`foo(self, x)`,为什么要这么做呢?因为实例方法的调用离不开实例,我们需要把实例自己传给函数,调用的时候是这样的`a.foo(x)`(其实是`foo(a, x)`).类方法一样,只不过它传递的是类而不是实例,`A.class_foo(x)`.注意这里的self和cls可以替换别的参数,但是python的约定是这俩,还是不要改的好.

对于静态方法其实和普通的方法一样,不需要对谁进行绑定,唯一的区别是调用的时候需要使用`a.static_foo(x)`或者`A.static_foo(x)`来调用.

| \\      | 实例方法     | 类方法            | 静态方法            |
| :------ | :------- | :------------- | :-------------- |
| a = A() | a.foo(x) | a.class_foo(x) | a.static_foo(x) |
| A       | 不可用      | A.class_foo(x) | A.static_foo(x) |

更多关于这个问题:
1. http://stackoverflow.com/questions/136097/what-is-the-difference-between-staticmethod-and-classmethod-in-python
2. https://realpython.com/blog/python/instance-class-and-static-methods-demystified/
## 4 类变量和实例变量

**类变量：**

> ​	是可在类的所有实例之间共享的值（也就是说，它们不是单独分配给每个实例的）。例如下例中，num_of_instance 就是类变量，用于跟踪存在着多少个Test 的实例。

**实例变量：**

> 实例化之后，每个实例单独拥有的变量。

```python
class Test(object):  
    num_of_instance = 0  
    def __init__(self, name):  
        self.name = name  
        Test.num_of_instance += 1  
  
if __name__ == '__main__':  
    print Test.num_of_instance   # 0
    t1 = Test('jack')  
    print Test.num_of_instance   # 1
    t2 = Test('lucy')  
    print t1.name , t1.num_of_instance  # jack 2
    print t2.name , t2.num_of_instance  # lucy 2
```

> 补充的例子

```python
class Person:
    name="aaa"

p1=Person()
p2=Person()
p1.name="bbb"
print p1.name  # bbb
print p2.name  # aaa
print Person.name  # aaa
```

这里`p1.name="bbb"`是实例调用了类变量,这其实和上面第一个问题一样,就是函数传参的问题,`p1.name`一开始是指向的类变量`name="aaa"`,但是在实例的作用域里把类变量的引用改变了,就变成了一个实例变量,self.name不再引用Person的类变量name了.

可以看看下面的例子:

```python
class Person:
    name=[]

p1=Person()
p2=Person()
p1.name.append(1)
print p1.name  # [1]
print p2.name  # [1]
print Person.name  # [1]
```

参考:http://stackoverflow.com/questions/6470428/catch-multiple-exceptions-in-one-line-except-block

## 5 Python自省

这个也是python彪悍的特性.

自省就是面向对象的语言所写的程序在运行时,所能知道对象的类型.简单一句就是运行时能够获得对象的类型.比如type(),dir(),getattr(),hasattr(),isinstance().

```python
a = [1,2,3]
b = {'a':1,'b':2,'c':3}
c = True
print type(a),type(b),type(c) # <type 'list'> <type 'dict'> <type 'bool'>
print isinstance(a,list)  # True
```



## 6 字典推导式

可能你见过列表推导时,却没有见过字典推导式,在2.7中才加入的:

```python
d = {key: value for (key, value) in iterable}
```

## 7 Python中单下划线和双下划线

```python
>>> class MyClass():
...     def __init__(self):
...             self.__superprivate = "Hello"
...             self._semiprivate = ", world!"
...
>>> mc = MyClass()
>>> print mc.__superprivate
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: myClass instance has no attribute '__superprivate'
>>> print mc._semiprivate
, world!
>>> print mc.__dict__
{'_MyClass__superprivate': 'Hello', '_semiprivate': ', world!'}
```

`__foo__`:一种约定,Python内部的名字,用来区别其他用户自定义的命名,以防冲突，就是例如`__init__()`,`__del__()`,`__call__()`这些特殊方法

`_foo`:一种约定,用来指定变量私有.程序员用来指定私有变量的一种方式.不能用from module import * 导入，其他方面和公有一样访问；

`__foo`:这个有真正的意义:解析器用`_classname__foo`来代替这个名字,以区别和其他类相同的命名,它无法直接像公有成员一样随便访问,通过对象名._类名__xxx这样的方式可以访问.

详情见:http://stackoverflow.com/questions/1301346/the-meaning-of-a-single-and-a-double-underscore-before-an-object-name-in-python

或者: http://www.zhihu.com/question/19754941

(1)、以单下划线开头，表示这是一个**保护成员**，只有类对象和子类对象自己能访问到这些变量。以单下划线开头的变量和函数被默认当作是内部函数，使用from module improt *时不会被获取，但是使用import module可以获取

(2)、以单下划线结尾仅仅是为了区别该名称与关键词

(3)、双下划线开头，表示为**私有成员**，只允许类本身访问，子类也不行。在文本上被替换为_class__method

(4)、双下划线开头，双下划线结尾。一种约定，Python内部的名字，用来区别其他用户自定义的命名,以防冲突。是一些 Python 的“魔术”对象，表示这是一个特殊成员，例如：定义类的时候，若是添加__init__方法，那么在创建类的实例的时候，实例会自动调用这个方法，一般用来对实例的属性进行初使化，Python不建议将自己命名的方法写为这种形式。

## 8 字符串格式化:%和.format

.format在许多方面看起来更便利.对于`%`最烦人的是它无法同时传递一个**变量**和**元组**.你可能会想下面的代码不会有什么问题:

```
"hi there %s" % name
```

但是,如果name恰好是(1,2,3),它将会抛出一个TypeError异常.为了保证它总是正确的,你必须这样做:

```
"hi there %s" % (name,)   # 提供一个单元素的数组而不是一个参数
```

但是有点丑..format就没有这些问题.你给的第二个问题也是这样,.format好看多了.

你为什么不用它?

* 不知道它(在读这个之前)
* 为了和Python2.5兼容(譬如logging库建议使用`%`([issue #4](https://github.com/taizilongxu/interview_python/issues/4)))

http://stackoverflow.com/questions/5082452/python-string-formatting-vs-format

## 9 迭代器和生成器

这个是stackoverflow里python排名第一的问题,值得一看: http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python

这是中文版: http://taizilongxu.gitbooks.io/stackoverflow-about-python/content/1/README.html

这里有个关于生成器的创建问题面试官有考：
问：  将列表生成式中[]改成() 之后数据结构是否改变？ 
答案：是，从列表变为生成器

```python
>>> L = [x*x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x*x for x in range(10))
>>> g
<generator object <genexpr> at 0x0000028F8B774200>
```
通过列表生成式，可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含百万元素的列表，不仅是占用很大的内存空间，如：我们只需要访问前面的几个元素，后面大部分元素所占的空间都是浪费的。因此，没有必要创建完整的列表（节省大量内存空间）。在Python中，我们可以采用生成器：边循环，边计算的机制—>generator

## 10 `*args` and `**kwargs`

用`*args`和`**kwargs`只是为了方便并没有强制使用它们.

当你不确定你的函数里将要传递多少参数时你可以用`*args`.例如,它可以传递任意数量的参数:

```python
>>> def print_everything(*args):
        for count, thing in enumerate(args):
...         print '{0}. {1}'.format(count, thing)
...
>>> print_everything('apple', 'banana', 'cabbage')
0. apple
1. banana
2. cabbage
```

相似的,`**kwargs`允许你使用没有事先定义的参数名:

```python
>>> def table_things(**kwargs):
...     for name, value in kwargs.items():
...         print '{0} = {1}'.format(name, value)
...
>>> table_things(apple = 'fruit', cabbage = 'vegetable')
cabbage = vegetable
apple = fruit
```

你也可以混着用.命名参数首先获得参数值然后所有的其他参数都传递给`*args`和`**kwargs`.命名参数在列表的最前端.例如:

```
def table_things(titlestring, **kwargs)
```

`*args`和`**kwargs`可以同时在函数的定义中,但是`*args`必须在`**kwargs`前面.

当调用函数时你也可以用`*`和`**`语法.例如:

```python
>>> def print_three_things(a, b, c):
...     print 'a = {0}, b = {1}, c = {2}'.format(a,b,c)
...
>>> mylist = ['aardvark', 'baboon', 'cat']
>>> print_three_things(*mylist)

a = aardvark, b = baboon, c = cat
```

就像你看到的一样,它可以传递列表(或者元组)的每一项并把它们解包.注意必须与它们在函数里的参数相吻合.当然,你也可以在函数定义或者函数调用时用*.

http://stackoverflow.com/questions/3394835/args-and-kwargs



函数中的参数

1. 函数中的四类参数
	必选参数，默认参数，可选参数，关键字参数
	def func(name, purpose="Demo", *args, kwargs)
		print(name)
		print(purpose)
		print(args)
		print(kwargs)
	例如上述函数中：
		name为必选参数，在函数或者类实例化的时候必须传入的，
		purpose为默认参数，在实例化时可以传也可以不传入，
		*args（positional arguments）为可选位置参数, 
		kwargs（kwargs: keyword arguments）可选关键字参数，kwargs的传入函数的类型是字典**
2. *和**的用途
   
    1. 用于对可迭代对象进行拆分
        在Python中，一切内置了iter方法的对象都是可迭代对象，典型的可迭代对象包括元组（tuple）、列表（list）、集合（set）、字典（dict）等等。这种拆解主要运用在函数的参数语境中，以print函数为例，以下5个表达式是完全等价的：但是要注意的是，集合不太一样，因为集合是无序的，所以print(*{"a", "b", "c"})的时候"a", "b", "c"可能是乱序的。
            print("a", "b", "c")                
            print(*("a", "b", "c"))             # 元组 
            print(*["a", "b", "c"])             # 列表
            print(*{"a": 1, "b": 2, "c": 3})    # 注意：对字典拆解时只拆解key
            print(*"abc")                       # 注意：字符串也是可迭代对象
    2. 可变变量的赋值
        如果对于一个可迭代对象l = [1, 2, 3, 4, 5, 6]，如果我想把第一个元素赋值给变量a，而把剩下的元素通通赋值给变量b，该怎么写呢？你可能会想这么写
            l = [1, 2, 3, 4, 5, 6]
            a = l[0]
            b = l[1:]
        这么写有两个问题：（一）设想一个更复杂的情况，如果我想把第一个元素赋值给变量a，最后一个元素赋值给c，而把剩下的元素统统赋值给变量b，那么代码将变得又臭又长；（二）这么写对于unsubscriptable的对象是不适用的，比如集合。用*可以非常优雅地解决这个问题，如：
            a, *b, c = {1, 2, 3, 4, 5, 6}
    3. 理解了前面两点，这一点其实就是上面两点的综合运用。如果是单星号*标记的就是可选的位置参数（positional arguments），如果是双星号标记的就是可选的关键词参数（keyword arguments），如:
            def function(a, *args, **kwargs):
                print(a)
                print(args)
                print(kwargs)
    
            function(1, 2, 3, c=4)
        输出结果如下：
            1
            (2, 3)
            {'c': 4}

## 11 面向切面编程AOP和装饰器

这个AOP一听起来有点懵,同学面阿里的时候就被问懵了...

装饰器是一个很著名的设计模式，经常被用于有切面需求的场景，较为经典的有插入日志、性能测试、事务处理等。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量函数中与函数功能本身无关的雷同代码并继续重用。概括的讲，**装饰器的作用就是为已经存在的对象添加额外的功能。**

这个问题比较大,推荐: http://stackoverflow.com/questions/739654/how-can-i-make-a-chain-of-function-decorators-in-python

中文: http://taizilongxu.gitbooks.io/stackoverflow-about-python/content/3/README.html

## 12 鸭子类型

“当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。”

我们并不关心对象是什么类型，到底是不是鸭子，只关心行为。

比如在python中，有很多file-like的东西，比如StringIO,GzipFile,socket。它们有很多相同的方法，我们把它们当作文件使用。

又比如list.extend()方法中,我们并不关心它的参数是不是list,只要它是可迭代的,所以它的参数可以是list/tuple/dict/字符串/生成器等.

鸭子类型在动态语言中经常使用，非常灵活，使得python不像java那样专门去弄一大堆的设计模式。

## 13 Python中重载

引自知乎:http://www.zhihu.com/question/20053359

函数重载主要是为了解决两个问题。

1. 可变参数类型。
2. 可变参数个数。

另外，一个基本的设计原则是，仅仅当两个函数除了参数类型和参数个数不同以外，其功能是完全相同的，此时才使用函数重载，如果两个函数的功能其实不同，那么不应当使用重载，而应当使用一个名字不同的函数。

好吧，那么对于情况 1 ，函数功能相同，但是参数类型不同，python 如何处理？答案是根本不需要处理，因为 python 可以接受任何类型的参数，如果函数的功能相同，那么不同的参数类型在 python 中很可能是相同的代码，没有必要做成两个不同函数。

那么对于情况 2 ，函数功能相同，但参数个数不同，python 如何处理？大家知道，答案就是缺省参数。对那些缺少的参数设定为缺省参数即可解决问题。因为你假设函数功能相同，那么那些缺少的参数终归是需要用的。

好了，鉴于情况 1 跟 情况 2 都有了解决方案，python 自然就不需要函数重载了。

## 14 新式类和旧式类

这个面试官问了,我说了老半天,不知道他问的真正意图是什么.

[stackoverflow](http://stackoverflow.com/questions/54867/what-is-the-difference-between-old-style-and-new-style-classes-in-python)

这篇文章很好的介绍了新式类的特性: http://www.cnblogs.com/btchenguang/archive/2012/09/17/2689146.html

在Python 2及以前的版本中，由任意内置类型派生出的类(只要一个内置类型位于类树的某个位置)，都属于“新式类”，都会获得所有“新式类”的特性；反之，即不由任意内置类型派生出的类，则称之为“经典类”。

“新式类”和“经典类”的区分在Python 3之后就已经不存在，在Python 3.x之后的版本，因为所有的类都派生自内置类型object(即使没有显示的继承[object类](https://so.csdn.net/so/search?q=object类&spm=1001.2101.3001.7020)型)，即所有的类都是“新式类”。

新式类很早在2.2就出现了,所以旧式类完全是兼容的问题,Python3里的类全部都是新式类.这里有一个MRO问题可以了解下(新式类继承是根据C3算法,旧式类是深度优先),<Python核心编程>里讲的也很多.

> 一个旧式类的深度优先的例子

```python
class A():
    def foo1(self):
        print "A"
class B(A):
    def foo2(self):
        pass
class C(A):
    def foo1(self):
        print "C"
class D(B, C):
    pass

d = D()
d.foo1()

# A
```

**按照经典类的查找顺序`从左到右深度优先`的规则，在访问`d.foo1()`的时候,D这个类是没有的..那么往上查找,先找到B,里面没有,深度优先,访问A,找到了foo1(),所以这时候调用的是A的foo1()，从而导致C重写的foo1()被绕过**

**什么是MRO**

所谓的MRO，就是方法解析顺序(Method Resolution Order)。在调用方法时，会对当前类以及所有的基类进行一个搜索，确定要调用的方法具体在哪。不管用哪种方式去确定MRO列表，必须满足 本地优先级和单调性。

本地优先级：指声明时父类的顺序，比如C(A,B)，如果访问C类对象属性时，应该根据声明顺序，优先查找A类，然后再查找B类

单调性：如果在C的解析顺序中，A排在B的前面，那么在C的所有子类里，也必须满足这个顺序
**常见MRO算法**

1. 深度优先遍历的(DFS)
2. 广度优先遍历的(BFS)
3. C3算法



## 15 `__new__`和`__init__`的区别

这个`__new__`确实很少见到,先做了解吧.

1. `__new__`是一个静态方法,而`__init__`是一个实例方法.
2. `__new__`方法会返回一个创建的实例,而`__init__`什么都不返回.
3. 只有在`__new__`返回一个cls的实例时后面的`__init__`才能被调用.
4. 当创建一个新实例时调用`__new__`,初始化一个实例时用`__init__`.

[stackoverflow](http://stackoverflow.com/questions/674304/pythons-use-of-new-and-init)

ps: `__metaclass__`是创建类时起作用.所以我们可以分别使用`__metaclass__`,`__new__`和`__init__`来分别在类创建,实例创建和实例初始化的时候做一些小手脚.

	1. __init__()通常用于初始化一个新实例，控制这个初始化的过程，比如添加一些属性，做一些额外的操作，发生在类实例被创建完以后。它是实例级别的方法。
	2. __new__()通常用于控制生成一个新实例的过程。它是类级别的方法。
	3. __new__()至少有一个参数cls，代表要实例化的类，此参数在实例化时会有python编辑器自动提供。
	4. __new__()必须有返回值，返回实例化出来的实例。如果__new__()没有返回cls（即当前类的实例），那么当前类的__init__()方法是不会被调用的，如果__new__()返回了其他类的实例，那么只会调用被返回的那个类的构造方法
		class A(object):
			def __init__(self, *args, **kwargs):
				print("run the init of A")
			def __new__(cls, *args, **kwargs):
				print("run thr new of A")
				return object.__new__(B, *args, **kwargs)
	
		class B(object):
			def __init__(self):
				print("run the init of B")
			def __new__(cls, *args, **kwargs):
				print("run the new of B")
				return object.__new__(cls)
		a = A()
		print(type(a))
		输出：
			run thr new of A
			<class '__main__.B'>
	        
		b = B()
		print(type(b))
		输出：
			run the new of B
			run the init of B
			<class '__main__.B'>
	5. 如果将类比作制造商，__new__()方法发就是前期的原材料环节，__init__()方法就是在有了原材料的基础上，加工，初始化商品的环节。

## 16 单例模式

> ​	单例模式是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例类的特殊类。通过单例模式可以保证系统中一个类只有一个实例而且该实例易于外界访问，从而方便对实例个数的控制并节约系统资源。如果希望在系统中某个类的对象只能存在一个，单例模式是最好的解决方案。
>
> `__new__()`在`__init__()`之前被调用，用于生成实例对象。利用这个方法和类的属性的特点可以实现设计模式的单例模式。单例模式是指创建唯一对象，单例模式设计的类只能实例
**这个绝对常考啊.绝对要记住1~2个方法,当时面试官是让手写的.**

### 1 使用`__new__`方法

```python
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            cls._instance = super().__new__(cls, *args, **kwargs)
        return cls._instance

class MyClass(Singleton):
    a = 1
```

### 2 共享属性

创建实例时把所有实例的`__dict__`指向同一个字典,这样它们具有相同的属性和方法.

```python

class Borg(object):
    _state = {}
    def __new__(cls, *args, **kw):
        ob = super(Borg, cls).__new__(cls, *args, **kw)
        ob.__dict__ = cls._state
        return ob

class MyClass2(Borg):
    a = 1
```

### 3 装饰器版本

```python
def singleton(cls):
    instances = {}
    def getinstance(*args, **kw):
        if cls not in instances:
            instances[cls] = cls(*args, **kw)
        return instances[cls]
    return getinstance

@singleton
class MyClass:
  ...
```

### 4 import方法

作为python的模块是天然的单例模式

```python
# mysingleton.py
class My_Singleton(object):
    def foo(self):
        pass

my_singleton = My_Singleton()

# to use
from mysingleton import my_singleton

my_singleton.foo()

```
**[单例模式伯乐在线详细解释](http://python.jobbole.com/87294/)**

## 17 Python中的作用域

Python 中，一个变量的作用域总是由在代码中被赋值的地方所决定的。

当 Python 遇到一个变量的话他会按照这样的顺序进行搜索：

本地作用域（Local）→当前作用域被嵌入的本地作用域（Enclosing locals）→全局/模块作用域（Global）→内置作用域（Built-in）



变量仅在创建区域内可用。 这称为作用域(scope)。

1. 局部作用域(Local Scope)。在函数内部创建的变量属于该函数的本地范围作用域(scope)，并且只能在该函数内部使用。

2. 全局作用域(Global Scope)。在Python代码主体中创建的变量是全局变量，属于全局范围。全局变量可以在任何作用域中使用，包括全局和局部作用域。

3. global全局关键字。如果需要在方法或函数内创建一个全局变量，则可以使用global关键字。global关键字使变量成为全局变量。要改变函数内部全局变量的值，可以使用global关键字引用该变量:

   ```python
   x = 300
   
   def myfunc():
       global x
       x = 200
   
   myfunc()
   
   print(x)
   ```

   

## 18 GIL线程全局锁

线程全局锁(Global Interpreter Lock),即Python为了保证线程安全而采取的独立线程运行的限制,说白了就是一个核只能在同一时间运行一个线程.**对于io密集型任务，python的多线程起到作用，但对于cpu密集型任务，python的多线程几乎占不到任何优势，还有可能因为争夺资源而变慢。**

见[Python 最难的问题](http://www.oschina.net/translate/pythons-hardest-problem)

解决办法就是多进程和下面的协程(协程也只是单CPU,但是能减小切换代价提升性能).

## 19 协程

知乎被问到了,呵呵哒,跪了

简单点说协程是进程和线程的升级版,进程和线程都面临着内核态和用户态的切换问题而耗费许多切换时间,而协程就是用户自己控制切换的时机,不再需要陷入系统的内核态.

Python里最常见的yield就是协程的思想!可以查看第九个问题.

**协程**，又称微线程，纤程。英文名Coroutine。协程的特点在于是一个线程执行。

1. 最大的优势就是协程极高的执行效率。因为子程序切换不是线程切换，而是由程序自身控制，因此，没有线程切换的开销，和多线程比，线程数量越多，协程的性能优势就越明显。

2. 第二大优势就是不需要多线程的锁机制，因为只有一个线程，也不存在同时写变量冲突，在协程中控制共享资源不加锁，只需要判断状态就好了，所以执行效率比多线程高很多。

因为协程是一个线程执行，那怎么利用多核CPU呢？最简单的方法是多进程+协程，既充分利用多核，又充分发挥协程的高效率，可获得极高的性能。


## 20 闭包

闭包(closure)是函数式编程的重要的语法结构。闭包也是一种组织代码的结构，它同样提高了代码的可重复使用性。

当一个内嵌函数引用其外部作作用域的变量,我们就会得到一个闭包. 总结一下,创建一个闭包必须满足以下几点:

1. 必须有一个内嵌函数
2. 内嵌函数必须引用外部函数中的变量
3. 外部函数的返回值必须是内嵌函数

感觉闭包还是有难度的,几句话是说不明白的,还是查查相关资料.

重点是函数运行后并不会被撤销,就像16题的instance字典一样,当函数运行完后,instance并不被销毁,而是继续留在内存空间里.这个功能类似类里的类变量,只不过迁移到了函数上.

闭包就像个空心球一样,你知道外面和里面,但你不知道中间是什么样.

闭包：

- 函数内的属性，都是由生命周期的，都是在函数执行期间
- 内部函数对外部函数作用域里变量的引用
- 闭包内的函数私有化了变量，完成了数据的封装，类似面向对象

```python
def func1(func): #外部函数
	a=1 #外部函数作用域里的变量
	print('this is func1')
	def func2(): #内部函数
		return func() # 返回func（）相当于引用了外部函数的变量，即传入的func
	return func2


@func1
def myprint():
	print('this is myprint')
myprint()


# 带参数的装饰器
def born(sex):
	def func1(fun):
		def warp():
			if sex=='man':
				print('你不可以生娃')
			if sex=='woman':
				print('你可以生娃')
			return fun()
		return warp
	return func1
@born(sex='man')
def man():
	print('好好上班')
@born(sex='woman')
def woman():
	print('好好上班')

man()
woman()
```



## 21 lambda函数

其实就是一个匿名函数,为什么叫lambda?因为和后面的函数式编程有关.

推荐: [知乎](http://www.zhihu.com/question/20125256)


## 22 Python函数式编程

这个需要适当的了解一下吧,毕竟函数式编程在Python中也做了引用.

推荐: [酷壳](http://coolshell.cn/articles/10822.html)

python中函数式编程支持:

filter 函数的功能相当于过滤器。调用一个布尔函数`bool_func`来迭代遍历每个seq中的元素；返回一个使`bool_seq`返回值为true的元素的序列。

```python
>>>a = [1,2,3,4,5,6,7]
>>>b = filter(lambda x: x > 5, a)
>>>print b
>>>[6,7]
```

map函数是对一个序列的每个项依次执行函数，下面是对一个序列每个项都乘以2：

```python
>>> a = map(lambda x:x*2,[1,2,3])
>>> list(a)
[2, 4, 6]
```

reduce函数是对一个序列的每个项迭代调用函数，下面是求3的阶乘：

```python
>>> reduce(lambda x,y:x*y,range(1,4))
6
```

## 23 Python里的拷贝

引用和copy(),deepcopy()的区别

- **直接赋值**：其实就是对象的引用（别名）。
- **浅拷贝(copy)**：拷贝父对象，不会拷贝对象的内部的子对象。浅拷贝， a 和 b 是一个独立的对象，但他们的子对象还是指向统一对象（是引用），所以它们的子对象变化同步，其他不同步。实际上，浅拷贝指的是重新分配一块内存，创建一个新的对象，但里面的元素是原对象中各个子对象的引用。
- **深拷贝(deepcopy)**： copy 模块的 deepcopy 方法，完全拷贝了父对象及其子对象。
- **注意：**需要指出的是，对于有些基本数据类型（如 int ，str），由于 Python 实际上采用的是引用计数的机制，情况有些不同。无论是怎样进行赋值或拷贝，只要是相同的值，就会指向同一个内存地址，实际上这时就是增加了一个引用计数。

```python
import copy
a = [1, 2, 3, 4, ['a', 'b']]  #原始对象

b = a  #赋值，传对象的引用
c = copy.copy(a)  #对象拷贝，浅拷贝
d = copy.deepcopy(a)  #对象拷贝，深拷贝

a.append(5)  #修改对象a
a[4].append('c')  #修改对象a中的['a', 'b']数组对象

print 'a = ', a
print 'b = ', b
print 'c = ', c
print 'd = ', d

输出结果：
a =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
b =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
c =  [1, 2, 3, 4, ['a', 'b', 'c']]
d =  [1, 2, 3, 4, ['a', 'b']]
```

## 24 Python垃圾回收机制

Python GC主要使用引用计数（reference counting）来跟踪和回收垃圾。在引用计数的基础上，通过“标记-清除”（mark and sweep）解决容器对象可能产生的循环引用问题，通过“分代回收”（generation collection）以空间换时间的方法提高垃圾回收效率。

### 1 引用计数

PyObject是每个对象必有的内容，其中`ob_refcnt`就是做为引用计数。当一个对象有新的引用时，它的`ob_refcnt`就会增加，当引用它的对象被删除，它的`ob_refcnt`就会减少.引用计数为0时，该对象生命就结束了。

优点:

1. 简单
2. 实时性

缺点:

1. 维护引用计数消耗资源
2. 循环引用

### 2 标记-清除机制

在了解标记清除算法前，我们需要明确一点，关于变量的存储，内存中有两块区域：堆区与栈区，在定义变量时，变量名与值内存地址的关联关系存放于栈区，变量值存放于堆区，内存管理回收的则是堆区的内容。

标记/清除算法的做法是当应用程序可用的内存空间被耗尽时，就会停止整个程序，然后进行两项工作，第一项则是标记，第二项则是清除。标记的过程就行相当于从栈区出发一条线，“连接”到堆区，再由堆区间接“连接”到其他地址，凡是被这条自栈区起始的线连接到内存空间都属于可以访达的，会被标记为存活。清除的过程将遍历堆中所有的对象，将没有标记存活的对象全部清除掉。

![img](https://pic3.zhimg.com/v2-1bfee07a84fc747da5980d990430d10a_r.jpg)

### 3 分代技术

基于引用计数的回收机制，每次回收内存，都需要把所有对象的引用计数都遍历一遍，这是非常消耗时间的，于是引入了分代回收来提高回收效率，分代回收采用的是用“空间换时间”的策略。

分代回收的整体思想是：将系统中的所有内存块根据其存活时间划分为不同的集合，每个集合就成为一个“代”，垃圾收集频率随着“代”的存活时间的增大而减小，存活时间通常利用经过几次垃圾回收来度量。分代指的是根据存活时间来为变量划分不同等级（也就是不同的代）。新定义的变量，放到新生代这个等级中，假设每隔1分钟扫描新生代一次，如果发现变量依然被引用，那么该对象的权重（权重本质就是个整数）加一，当变量的权重大于某个设定得值（假设为3），会将它移动到更高一级的青春代，青春代的gc扫描的频率低于新生代（扫描时间间隔更长），假设5分钟扫描青春代一次，这样每次gc需要扫描的变量的总个数就变少了，节省了扫描的总时间，接下来，青春代中的对象，也会以同样的方式被移动到老年代中。也就是等级（代）越高，被垃圾回收机制扫描的频率越低

Python默认定义了三代对象集合，索引数越大，对象存活时间越长。

虽然分代回收可以起到提升效率的效果，但也存在一定的缺点。例如一个变量刚刚从新生代移入青春代，该变量的绑定关系就解除了，该变量应该被回收，但青春代的扫描频率低于新生代，所以该变量的回收就会被延迟。

举例：
当某些内存块M经过了3次垃圾收集的清洗之后还存活时，我们就将内存块M划到一个集合A中去，而新分配的内存都划分到集合B中去。当垃圾收集开始工作时，大多数情况都只对集合B进行垃圾回收，而对集合A进行垃圾回收要隔相当长一段时间后才进行，这就使得垃圾收集机制需要处理的内存少了，效率自然就提高了。在这个过程中，集合B中的某些内存块由于存活时间长而会被转移到集合A中，当然，集合A中实际上也存在一些垃圾，这些垃圾的回收会因为这种分代的机制而被延迟。

**概述：引用计数为主，标记清除，分代回收为辅**

**1引用计数**

**python程序中创建的所有的对象都是放在一个双向环状循环链表refchain上的**

如下对象被创建时，在C语言底层实际结构

name='string'

c语言内底部创建成 [上一个对象，下一个对象，类型，引用个数]

age=18

c语言内底部创建成[上一个对象，下一个对象，类型，引用个数，val=18]

hobby=['篮球'， '撸铁'，‘玩’]

c语言内底部创建成[上一个对象，下一个对象，类型，引用个数，item=元素， 元素个数]

当python程序运行时，会根据数据类型的不同找到其对应的结构体，根据结构体中的字段来进行创建相关的数据，然后将对象添加到refchain双向链表中

每个对象中有ob_refcnt就是应用计数器，默认为1，当有其他变量引用对象时，引用计数器就会+1

当引用计数器为0时，意味着没人使用这个对象了，这个对象就是垃圾，就会回收

**回收步骤**：1对象从refchain链表移除 2将对象销毁，内存回收

**2 标记清除**

**为什么要标记清除**：为了解决引用计数器循环引用的不足，循环引用可能导致内存泄漏

实现：在python的底层，再维护一个链表，链表中专门放那些可能存在循环引用的对象(list/tuple/dict/set)

在python内部，某种情况下触发，回去扫描可能存在循环引用链表中的每个元素，检查是否是循环引用，如果有，则让双方的引用计数器-1，如果是0，则垃圾回收

**3 分代回收**

**为什么要分代回收：**不知道什么情况下触发扫描，可能存在循环引用的链表扫描代价大，每次扫描很久

将可能存在循环引用的对象维护成3个链表

0代：0代中对象个数达到700个扫描一次

1代：0代扫描10次，则1代扫描1次

2代：1代扫描10次，则2代扫描1次

过程：当我们创建了一个对象a=1,这个对象只会加到refchain链表中，而当我们创建了一个可能存在循环引用的对象b=[]一个列表时，这个对象不但会加到refchain链表中，还会加到分带回收的0代链表中，当0代链表中对象达到700个，GC开始扫描，如果是循环引用，那就自减1，减完以后，如果是垃圾，那就自动回收，如果不是垃圾，那就将这些对象升级到1代链表中，就这样扫描一遍，此时0代链表也会记录自己扫描了1次，等到下次0代链表的对象又达到了700个，继续上述步骤，就这样执行了10次，才会触发执行扫描1代链表，1代链表和2代链表中的操作和0代中一样。

**4 小结(面试可以这么说)**

在python中，维护了一个refchain的双向循环环状链表，这个链表中存储程序创建的所有对象，每种类型的对象中都有一个ob_refcnt引用计数器的值，默认为1，当引用计数器变为0时会进行垃圾回收(对象销毁，refchain中移除)

但是，在python 中，对于那些可以有多个元素组成的对象可能会存在循环引用的问题，为了解决这个问题，python又引入了标记清除和分代回收，在其内部维护了四个链表

refchain 

0代 700个对象触发

1代 0代十次执行一次1代

2代 1代十次执行一次2代

当 每个链表达到阈值时，就会触发扫描链表进行标记清除操作，有循环则各自-1，为0时，直接回收，销毁，清除

But, 在上面的垃圾回收机制的步骤中，python提供了优化机制

## 25 Python的List

推荐: http://www.jianshu.com/p/J4U6rR

当创建一个列表时，在C语言底层会创建一个结构体来保存列表的数据：

```c
typedef struct {
    struct_object *_ob_next;
    struct_object *_ob_prev;    //双向环状列表中的上一个和下一个对象，python内部将对象放到链表中便于管理
    Py_ssize_t ob_refcnt;       // 引用计数器，
    PyObject **ob_item; 		//指针的引用，用于存放列表中的元素（内部用realloc来开辟内存）
    Py_ssize_t ob_size;  		//列表中元素已占的容量，即：当前列表中元素的个数
    Py_ssize_t allocated;		// 列表的容量，即：当前为列表开辟的容量最多容纳多少元素
} PyListObject;
```

![image-20221113154004852](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113154004852.png)

```c
PyObject *
PyList_New(Py_ssize_t size)
{
    PyListObject *op;
    size_t nbytes;
#ifdef SHOW_ALLOC_COUNT
    static int initialized = 0;
    if (!initialized) {
        Py_AtExit(show_alloc);
        initialized = 1;
    }
#endif
    // 缓存机制
    if (size < 0) {
        PyErr_BadInternalCall();
        return NULL;
    }
    /* Check for overflow without an actual overflow,
     *  which can cause compiler to optimise out */
    if ((size_t)size > PY_SIZE_MAX / sizeof(PyObject *))
        return PyErr_NoMemory();
    nbytes = size * sizeof(PyObject *);
    // 先从free_list中看是否有缓存的列表
    if (numfree) {
        numfree--;
        op = free_list[numfree];
        _Py_NewReference((PyObject *)op);
#ifdef SHOW_ALLOC_COUNT
        count_reuse++;
#endif
    } else {
        op = PyObject_GC_New(PyListObject, &PyList_Type);
        if (op == NULL)
            return NULL;Py
#ifdef SHOW_ALLOC_COUNT
        count_alloc++;
#endif
    }

    if (size <= 0)
        op->ob_item = NULL;
    else {
        op->ob_item = (PyObject **) PyMem_MALLOC(nbytes);
        if (op->ob_item == NULL) {
            Py_DECREF(op);
            return PyErr_NoMemory();
        }
        memset(op->ob_item, 0, nbytes);
    }
    Py_SIZE(op) = size;  // 元素个数
    op->allocated = size;   // 容量
    _PyObject_GC_TRACK(op); //放到双向链表进行维护
    return (PyObject *) op; //返回列表的指针
}

```



![image-20221113154754731](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113154754731.png)

```c
// 添加元素
static int
app1(PyListObject *self, PyObject *v)
{
    // 获取实际元素个数
    Py_ssize_t n = PyList_GET_SIZE(self);

    assert (v != NULL);
    if (n == PY_SSIZE_T_MAX) {
        PyErr_SetString(PyExc_OverflowError,
            "cannot add more objects to list");
        return -1;
    }

    // 计算当前容量和内部元素个数
    // 直接添加元素/扩容添加
    if (list_resize(self, n+1) == -1)
        return -1;
    // 将元素添加到ob_item，v
    Py_INCREF(v);
    PyList_SET_ITEM(self, n, v);
    return 0;
}

```

扩容

```c
// 扩容机制
 // newsize: 已存在元素个数+1
static int
list_resize(PyListObject *self, Py_ssize_t newsize)
{
    PyObject **items;
    size_t new_allocated;
    Py_ssize_t allocated = self->allocated; // 当前的容量

    // 1,容量大于个数
    // 2,个数大于容量的一半（容量足够且没有内存浪费）
    if (allocated >= newsize && newsize >= (allocated >> 1)) {
        assert(self->ob_item != NULL || newsize == 0);
        Py_SIZE(self) = newsize;
        return 0;
    }
	// 如果容量<元素个数+1,则表示容量不够，要进行重新扩容（开辟内存）
    // 如果元素个数+1<容量的一半，则表示容量太大会浪费空间，要进行缩减容量（减少内存）
    /* 
     * The growth pattern is:  0, 4, 8, 16, 25, 35, 46, 58, 72, 88, ...
     */
     // 扩容机制的算法
    new_allocated = (newsize >> 3) + (newsize < 9 ? 3 : 6);

    /* check for integer overflow */
    if (new_allocated > PY_SIZE_MAX - newsize) {
        PyErr_NoMemory();
        return -1;
    } else {
        new_allocated += newsize;
    }

    if (newsize == 0)
        new_allocated = 0;
    // 扩容/缩容（涉及原来元素的迁移）
    items = self->ob_item;
    if (new_allocated <= (PY_SIZE_MAX / sizeof(PyObject *)))
        PyMem_RESIZE(items, PyObject *, new_allocated);
    else
        items = NULL;
    if (items == NULL) {
        PyErr_NoMemory();
        return -1;
    }
    // 赋值，更新个数和容量
    self->ob_item = items;
    Py_SIZE(self) = newsize;
    self->allocated = new_allocated;
    return 0;
}

```

![image-20221113161008655](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113161008655.png)

![image-20221113161126471](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113161126471.png)

```c
static int
ins1(PyListObject *self, Py_ssize_t where, PyObject *v)
{
    // 获取元素个数
    Py_ssize_t i, n = Py_SIZE(self);
    PyObject **items;
    if (v == NULL) {
        PyErr_BadInternalCall();
        return -1;
    }
    if (n == PY_SSIZE_T_MAX) {
        PyErr_SetString(PyExc_OverflowError,
            "cannot add more objects to list");
        return -1;
    }
	// 重新计算容量是否可以支持新加入元素，扩容或者缩容
    if (list_resize(self, n+1) == -1)
        return -1;

    if (where < 0) {
        where += n;
        if (where < 0)
            where = 0;
    }
    if (where > n)
        where = n;
    items = self->ob_item;
    // 让插入位置之后的所有元素向后移动一个位置，腾出位置来插入数据
    for (i = n; --i >= where; )
        items[i+1] = items[i];
    Py_INCREF(v);
    // 插入新值
    items[where] = v;
    return 0;
}
```

pop()移除最后一个元素，删除最后一个元素只需要修改size，不需要清除数据，下次append可以直接覆盖这个位置。如果指定移除位置pop(2)，则会将原数据删除并移动其他元素补位。

![image-20221113161740585](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113161740585.png)

```c
static PyObject *
listpop(PyListObject *self, PyObject *args)
{
    Py_ssize_t i = -1;
    PyObject *v;
    int status;

    if (!PyArg_ParseTuple(args, "|n:pop", &i))
        return NULL;

    if (Py_SIZE(self) == 0) {
        /* Special-case most common failure cause */
        PyErr_SetString(PyExc_IndexError, "pop from empty list");
        return NULL;
    }
    if (i < 0)
        i += Py_SIZE(self);
    if (i < 0 || i >= Py_SIZE(self)) {
        PyErr_SetString(PyExc_IndexError, "pop index out of range");
        return NULL;
    }
    // 找到制动索引的位置
    v = self->ob_item[i];
    // 如果删除的是最后一个
    if (i == Py_SIZE(self) - 1) {
        // 重新计算容量和大小，其实内部主要size-1就好，也就表示最后一个数据不再包括在item中。
        // 后期再添加的时候，直接把里面的内存地址替换掉即可。
        status = list_resize(self, Py_SIZE(self) - 1);
        assert(status >= 0);
        return v; /* and v now owns the reference the list had */
    }
    Py_INCREF(v);
    // 如果删除的不是最后一个元素，则需要移动相关的数据位置
    status = list_ass_slice(self, i, i+1, (PyObject *)NULL);
    assert(status >= 0);
    /* Use status, so that in a release build compilers don't
     * complain about the unused name.
     */
    (void) status;

    return v;
}
```

清空元素，只需要size=0，allocated=0，item=NULL

![image-20221113162947815](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113162947815.png)

```c
static int
list_clear(PyListObject *a)
{
    Py_ssize_t i;
    PyObject **item = a->ob_item;
    if (item != NULL) {
        i = Py_SIZE(a);
        // 各个元素设置为空
        Py_SIZE(a) = 0;
        a->ob_item = NULL;
        a->allocated = 0;
        // 将列表中各元素的引用计数器-1
        while (--i >= 0) {
            Py_XDECREF(item[i]);
        }
        PyMem_FREE(item);
    }
 
    return 0;
}
```

6.销毁

del list

销毁列表对象的操作
首先，将列表的引用计数-1

1. 引用计数>0，表示还有其他变量使用此列表，之后不做操作
2. 引用计数=0，没人使用，需做如下事宜：
   1. 如果列表中有数据，则先处理元素，找到每个元素，将元素的引用计数器-1（如果元素的引用计数器为0，则元素可以被GC回收）
   2. 处理完元素后，size=0，allocated=0，item=NULL
   3. 将列表从管理内存的双向环状列表中移除，认为这个对象没人使用了，现在可以被销毁了
   4. python为了提高效率，在内部为`free_list`可以缓存80个列表，当有些列表没人使用后不会立即销毁，而是放在free_list中，以便再创建列表对象时可以直接从缓存中拿到列表的结构体对象并重新初始化，然后再来使用。如果free_list中已经存了80个，再有列表销毁时，将会直接在内存中销毁。

```c
/* Empty list reuse scheme to save calls to malloc and free */
#ifndef PyList_MAXFREELIST
#define PyList_MAXFREELIST 80
#endif
static PyListObject *free_list[PyList_MAXFREELIST];
static int numfree = 0;

static void
list_dealloc(PyListObject *op)
{
    Py_ssize_t i;
    // 判断引用计数器的个数，如果是0，则意味着没人使用，可以从内部维护的链表中移除
    PyObject_GC_UnTrack(op);
    Py_TRASHCAN_SAFE_BEGIN(op)
    if (op->ob_item != NULL) {
        /* Do it backwards, for Christian Tismer.
           There's a simple test case where somehow this reduces
           thrashing when a *very* large list is created and
           immediately deleted. */
        i = Py_SIZE(op);
        while (--i >= 0) {
            Py_XDECREF(op->ob_item[i]);
        }
        PyMem_FREE(op->ob_item);
    }
    // 如果缓存的free_list中没有满80个，则不在内存销毁列表结构体对象，放入free_list中缓存起来，以便后续创建列表用
    if (numfree < PyList_MAXFREELIST && PyList_CheckExact(op))
        free_list[numfree++] = op;
    else
        // 如果满80，则在内存中销毁这个列表的结构体对象
        Py_TYPE(op)->tp_free((PyObject *)op);
    Py_TRASHCAN_SAFE_END(op)
}
```

注意：在创建列表时，其实不会直接开辟内存，而是先从free_list中看有么有缓存的列表对象。

![image-20221113170108738](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221113170108738.png)

来源：[python列表底层原理剖析（基于c源码学python list 内部实现）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1wh411D7Nx/)

## 26 Python的is

Python 中对象包含的三个基本要素，分别是：id(身份标识)、type(数据类型)和value(值)。

- == 是python标准操作符中的比较操作符，用来比较判断两个对象的 value (值) 是否相等。
- is 也被叫做同一性运算符，这个运算符比较判断的是对象间的唯一身份标识，也就是说它判断的是两个对象的 id是否相同

## 27 read,readline和readlines

* read        读取整个文件
* readline    读取下一行,使用生成器方法
* readlines   读取整个文件到一个迭代器以供我们遍历

## 28 Python2和3的区别
推荐：[Python 2.7.x 与 Python 3.x 的主要差异](http://chenqx.github.io/2014/11/10/Key-differences-between-Python-2-7-x-and-Python-3-x/)

**print函数**

整除

```python
# python2
3/2 
# 输出1
```

```python
# python3
3/2
# 输出1.5
```



**unicode**：Python 2 有 ASCII str() 类型，`unicode()` 是单独的，不是 `byte` 类型。现在， 在 Python 3，我们最终有了 `Unicode (utf-8)` 字符串，以及一个字节类：`byte` 和 `bytearrays`。

**xrange模块：**

**Raising exceptions：**Python 2 接受新旧两种语法标记，在 Python 3 中如果我不用小括号把异常参数括起来就会阻塞（并且反过来引发一个语法异常）。

```python
#python2	
raise IOError, "file error"
```

```python
# python3
raise IOError("file error")
```

**Handling exceptions：**在 Python 3 中我们现在使用 as 作为关键词。

```python
# python2
try:
    let_us_cause_a_NameError
except NameError, err:
    print err, '--> our error message'
```

```python
# python3
try:
    let_us_cause_a_NameError
except NameError as err:
    print(err, '--> our error message')
```

**next()函数 and .next()方法**：在 Python 2.7.5 中函数和方法你都可以使用，next() 函数在 Python 3 中一直保留着（调用 .next() 抛出属性异常）

```python
# python2
my_generator = (letter for letter in 'abcdefg')
next(my_generator)
my_generator.next()
```

```python
# python3
my_generator = (letter for letter in 'abcdefg')
next(my_generator)
# my_generator.next()会报错
# AttributeError: 'generator' object has no attribute 'next'
```

**For循环变量和全局命名空间泄漏：**在 Python 3.x 中 for 循环变量不会再导致命名空间泄漏。

```python
# python2
i = 1
print 'before: i =', i
print 'comprehension: ', [i for i in range(5)]
print 'after: i =', i
# 输出结果
before: i = 1
comprehension: [0, 1, 2, 3, 4]
after: i = 4
```

```python
i = 1
print('before: i =', i)
print('comprehension:', [i for i in range(5)])
print('after: i =', i)
# 输出结果
before: i = 1
comprehension: [0, 1, 2, 3, 4]
after: i = 1
```

**比较不可排序类型**：在 Python 3 中的另外一个变化就是当对不可排序类型做比较的时候，会抛出一个类型错误。

**通过input()解析用户的输入**：在 Python 3 中已经解决了把用户的输入存储为一个 str 对象的问题。为了避免在 Python 2 中的读取非字符串类型的危险行为，我们不得不使用 raw_input() 代替。

```python
>>> my_input = input('enter a number: ')

enter a number: 123

>>> type(my_input)
<type 'int'>

>>> my_input = raw_input('enter a number: ')

enter a number: 123

>>> type(my_input)
<type 'str'>
```

**返回可迭代对象，而不是列表**

```python
# python2
print range(3) 
print type(range(3))
# 结果
[0, 1, 2]
< type ‘list’>
```

```python
# python3
print(range(3))
print(type(range(3)))
print(list(range(3)))
# 输出结果
range(0, 3)
< class ‘range’>
[0, 1, 2]
在 Python 3 中一些经常使用到的不再返回列表的函数和方法：
zip()
map()
filter()
dictionary’s .keys() method
dictionary’s .values() method
dictionary’s .items() method
```



## 29 super init
super() lets you avoid referring to the base class explicitly, which can be nice. But the main advantage comes with multiple inheritance, where all sorts of fun stuff can happen. See the standard docs on super if you haven't already.

Note that the syntax changed in Python 3.0: you can just say super().`__init__`() instead of super(ChildB, self).`__init__`() which IMO is quite a bit nicer.

http://stackoverflow.com/questions/576169/understanding-python-super-with-init-methods

[Python2.7中的super方法浅见](http://blog.csdn.net/mrlevo520/article/details/51712440)

**super的使用**

在python2中super必须写出完整形式，例如super(Male,self)，而python3中可以使用super()

super的完整使用形式：super(class,class/obj)，有两个参数

1. 第一个参数：是一个type 也可以是一个class，第一个参数决定了在mro链上从哪个class后开始寻找
2. 第二个参数是一个type或者是一个object，第二个参数决定了这一个函数bind到哪一个object或者class上，同时第二个参数决定了使用哪个mro

```python
class Animal:
    def __init__(self,age):
        self.age=age
        
class Person(Animal):
    def __init__(self,age,name):
        super().__init__(age)
        self.name=name
        
class Male(Person):
    def __init__(self,age,name,male):
        # super().__init__(age,name)
        super(Male,self).__init__(age,name)
        self.gender=male
        
m=Male('Perter')
# super(Male,m).__init__(18,'per')
```

super并不是只能在class内使用，可以在任何一个地方使用，只要给定两个参数就可以使用。

如果不给定两个参数，则super只能在class内使用。python的魔法函数自动做了两件事：

1. 它会寻找自己是在哪个class里定义的，然后把这个class放到第一个参数上
2. 它会寻找自己是在哪个函数里定义的，然后把这个函数的第一个参数也就是self放到第二个参数上，所以super()等价于super(Male,self)

## 30 range and xrange
都在循环时使用，xrange内存性能更好。
for i in range(0, 20):
for i in xrange(0, 20):
What is the difference between range and xrange functions in Python 2.X?
 range creates a list, so if you do range(1, 10000000) it creates a list in memory with 9999999 elements.
 xrange is a sequence object that evaluates lazily.

http://stackoverflow.com/questions/94935/what-is-the-difference-between-range-and-xrange-functions-in-python-2-x

只有在python2中才有range和xrange函数，在python3中只有range函数。

python2中range函数返回的是一个列表，这样会占用大量的内存。而xrange返回的是一个可迭代对象的生成器。可以边循环边创建，这样节省内存提高性能。python3 中的range函数主要是python2中的xrange函数。

## 31 基本数据类型

不可变数据：Number(数字）、String(字符串）、Tuple(元组）；

可变数据：List（列表）、Dictionary（字典）、Set（集合）

# 操作系统

## 1 select,poll和epoll

其实所有的I/O都是轮询的方法,只不过实现的层面不同罢了.

这个问题可能有点深入了,但相信能回答出这个问题是对I/O多路复用有很好的了解了.其中tornado使用的就是epoll的.

[selec,poll和epoll区别总结](http://www.cnblogs.com/Anker/p/3265058.html)

基本上select有3个缺点:

1. 连接数受限
2. 查找配对速度慢
3. 数据由内核拷贝到用户态

poll改善了第一个缺点

epoll改了三个缺点.

关于epoll的: http://www.cnblogs.com/my_life/articles/3968782.html

## 2 调度算法

1. 先来先服务(FCFS, First Come First Serve)
2. 短作业优先(SJF, Shortest Job First)
3. 最高优先权调度(Priority Scheduling)
4. 时间片轮转(RR, Round Robin)
5. 多级反馈队列调度(multilevel feedback queue scheduling)

常见的调度算法总结:http://www.jianshu.com/p/6edf8174c1eb

实时调度算法:

1. 最早截至时间优先 EDF
2. 最低松弛度优先 LLF

## 3 死锁
原因:

1. 竞争资源
2. 程序推进顺序不当

必要条件:

1. 互斥条件
2. 请求和保持条件
3. 不剥夺条件
4. 环路等待条件

处理死锁基本方法:

1. 预防死锁(摒弃除1以外的条件)
2. 避免死锁(银行家算法)
3. 检测死锁(资源分配图)
4. 解除死锁
    1. 剥夺资源
    2. 撤销进程

死锁概念处理策略详细介绍:https://wizardforcel.gitbooks.io/wangdaokaoyan-os/content/10.html

## 4 程序编译与链接

推荐: http://www.ruanyifeng.com/blog/2014/11/compiler.html

Bulid过程可以分解为4个步骤:预处理(Prepressing), 编译(Compilation)、汇编(Assembly)、链接(Linking)

以c语言为例:

### 1 预处理

预编译过程主要处理那些源文件中的以“#”开始的预编译指令，主要处理规则有：

1. 将所有的“#define”删除，并展开所用的宏定义
2. 处理所有条件预编译指令，比如“#if”、“#ifdef”、 “#elif”、“#endif”
3. 处理“#include”预编译指令，将被包含的文件插入到该编译指令的位置，注：此过程是递归进行的
4. 删除所有注释
5. 添加行号和文件名标识，以便于编译时编译器产生调试用的行号信息以及用于编译时产生编译错误或警告时可显示行号
6. 保留所有的#pragma编译器指令。

### 2 编译

编译过程就是把预处理完的文件进行一系列的词法分析、语法分析、语义分析及优化后生成相应的汇编代码文件。这个过程是整个程序构建的核心部分。

### 3 汇编

汇编器是将汇编代码转化成机器可以执行的指令，每一条汇编语句几乎都是一条机器指令。经过编译、链接、汇编输出的文件成为目标文件(Object File)

### 4 链接

链接的主要内容就是把各个模块之间相互引用的部分处理好，使各个模块可以正确的拼接。
链接的主要过程包块 地址和空间的分配（Address and Storage Allocation）、符号决议(Symbol Resolution)和重定位(Relocation)等步骤。

## 5 静态链接和动态链接

静态链接方法：静态链接的时候，载入代码就会把程序会用到的动态代码或动态代码的地址确定下来
静态库的链接可以使用静态链接，动态链接库也可以使用这种方法链接导入库

动态链接方法：使用这种方式的程序并不在一开始就完成动态链接，而是直到真正调用动态库代码时，载入程序才计算(被调用的那部分)动态代码的逻辑地址，然后等到某个时候，程序又需要调用另外某块动态代码时，载入程序又去计算这部分代码的逻辑地址，所以，这种方式使程序初始化时间较短，但运行期间的性能比不上静态链接的程序

## 6 虚拟内存技术

虚拟存储器是指具有请求调入功能和置换功能,能从逻辑上对内存容量加以扩充的一种存储系统.

## 7 分页和分段

分页: 用户程序的地址空间被划分成若干固定大小的区域，称为“页”，相应地，内存空间分成若干个物理块，页和块的大小相等。可将用户程序的任一页放在内存的任一块中，实现了离散分配。

分段: 将用户程序地址空间分成若干个大小不等的段，每段可以定义一组相对完整的逻辑信息。存储分配时，以段为单位，段与段在内存中可以不相邻接，也实现了离散分配。

### 分页与分段的主要区别

1. 页是信息的物理单位,分页是为了实现非连续分配,以便解决内存碎片问题,或者说分页是由于系统管理的需要.段是信息的逻辑单位,它含有一组意义相对完整的信息,分段的目的是为了更好地实现共享,满足用户的需要.
2. 页的大小固定,由系统确定,将逻辑地址划分为页号和页内地址是由机器硬件实现的.而段的长度却不固定,决定于用户所编写的程序,通常由编译程序在对源程序进行编译时根据信息的性质来划分.
3. 分页的作业地址空间是一维的.分段的地址空间是二维的.

## 8 页面置换算法

1. 最佳置换算法OPT:不可能实现
2. 先进先出FIFO
3. 最近最久未使用算法LRU:最近一段时间里最久没有使用过的页面予以置换.
4. clock算法

## 9 边沿触发和水平触发

边缘触发是指每当状态变化时发生一个 io 事件，条件触发是只要满足条件就发生一个 io 事件

# 数据库

## 1 事务

数据库事务(Database Transaction) ，是指作为单个逻辑工作单元执行的一系列操作，要么完全地执行，要么完全地不执行。
彻底理解数据库事务: http://www.hollischuang.com/archives/898

## 2 数据库索引

推荐: http://tech.meituan.com/mysql-index.html

[MySQL索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)

聚集索引,非聚集索引,B-Tree,B+Tree,最左前缀原理

## 3 Redis原理

### Redis是什么？

1. 是一个完全开源免费的key-value内存数据库 
2. 通常被认为是一个数据结构服务器，主要是因为其有着丰富的数据结构 strings、map、 list、sets、 sorted sets

### Redis数据库

> ​	通常局限点来说，Redis也以消息队列的形式存在，作为内嵌的List存在，满足实时的高并发需求。在使用缓存的时候，redis比memcached具有更多的优势，并且支持更多的数据类型，把redis当作一个中间存储系统，用来处理高并发的数据库操作

- 速度快：使用标准C写，所有数据都在内存中完成，读写速度分别达到10万/20万 
- 持久化：对数据的更新采用Copy-on-write技术，可以异步地保存到磁盘上，主要有两种策略，一是根据时间，更新次数的快照（save 300 10 ）二是基于语句追加方式(Append-only file，aof) 
- 自动操作：对不同数据类型的操作都是自动的，很安全 
- 快速的主--从复制，官方提供了一个数据，Slave在21秒即完成了对Amazon网站10G key set的复制。 
- Sharding技术： 很容易将数据分布到多个Redis实例中，数据库的扩展是个永恒的话题，在关系型数据库中，主要是以添加硬件、以分区为主要技术形式的纵向扩展解决了很多的应用场景，但随着web2.0、移动互联网、云计算等应用的兴起，这种扩展模式已经不太适合了，所以近年来，像采用主从配置、数据库复制形式的，Sharding这种技术把负载分布到多个特理节点上去的横向扩展方式用处越来越多。

### Redis缺点

- 是数据库容量受到物理内存的限制,不能用作海量数据的高性能读写,因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。
- Redis较难支持在线扩容，在集群容量达到上限时在线扩容会变得很复杂。为避免这一问题，运维人员在系统上线时必须确保有足够的空间，这对资源造成了很大的浪费。

### redis做秒杀场景中的问题

1. 连接超时问题

   连接池

2. 多卖问题

   用watch乐观锁

3. 库存问题（少卖）

   lua脚本


## 4 乐观锁和悲观锁

悲观锁：假定会发生并发冲突，屏蔽一切可能违反数据完整性的操作

乐观锁：假设不会发生并发冲突，只在提交操作时检查是否违反数据完整性。

乐观锁与悲观锁的具体区别: http://www.cnblogs.com/Bob-FD/p/3352216.html

## 5 MVCC


> ​	全称是Multi-Version Concurrent Control，即多版本并发控制，在MVCC协议下，每个读操作会看到一个一致性的snapshot，并且可以实现非阻塞的读。MVCC允许数据具有多个版本，这个版本可以是时间戳或者是全局递增的事务ID，在同一个时间点，不同的事务看到的数据是不同的。

### [MySQL](http://lib.csdn.net/base/mysql)的innodb引擎是如何实现MVCC的

innodb会为每一行添加两个字段，分别表示该行**创建的版本**和**删除的版本**，填入的是事务的版本号，这个版本号随着事务的创建不断递增。在repeated read的隔离级别（[事务的隔离级别请看这篇文章](http://blog.csdn.net/chosen0ne/article/details/10036775)）下，具体各种数据库操作的实现：

- select：满足以下两个条件innodb会返回该行数据：
  - 该行的创建版本号小于等于当前版本号，用于保证在select操作之前所有的操作已经执行落地。
  - 该行的删除版本号大于当前版本或者为空。删除版本号大于当前版本意味着有一个并发事务将该行删除了。
- insert：将新插入的行的创建版本号设置为当前系统的版本号。
- delete：将要删除的行的删除版本号设置为当前系统的版本号。
- update：不执行原地update，而是转换成insert + delete。将旧行的删除版本号设置为当前版本号，并将新行insert同时设置创建版本号为当前版本号。

其中，写操作（insert、delete和update）执行时，需要将系统版本号递增。

​	由于旧数据并不真正的删除，所以必须对这些数据进行清理，innodb会开启一个后台线程执行清理工作，具体的规则是将删除版本号小于当前系统版本的行删除，这个过程叫做purge。

通过MVCC很好的实现了事务的隔离性，可以达到repeated read级别，要实现serializable还必须加锁。

>  参考：[MVCC浅析](http://blog.csdn.net/chosen0ne/article/details/18093187)



## 6 MyISAM和InnoDB

MyISAM 适合于一些需要大量查询的应用，但其对于有大量写操作并不是很好。甚至你只是需要update一个字段，整个表都会被锁起来，而别的进程，就算是读进程都无法操作直到读操作完成。另外，MyISAM 对于 SELECT COUNT(*) 这类的计算是超快无比的。

InnoDB 的趋势会是一个非常复杂的存储引擎，对于一些小的应用，它会比 MyISAM 还慢。他是它支持“行锁” ，于是在写操作比较多的时候，会更优秀。并且，他还支持更多的高级应用，比如：事务。

mysql 数据库引擎: http://www.cnblogs.com/0201zcr/p/5296843.html
MySQL存储引擎－－MyISAM与InnoDB区别: https://segmentfault.com/a/1190000008227211

# 网络

## 1 三次握手

1. 客户端通过向服务器端发送一个SYN来创建一个主动打开，作为三次握手的一部分。客户端把这段连接的序号设定为随机数 A。
2. 服务器端应当为一个合法的SYN回送一个SYN/ACK。ACK 的确认码应为 A+1，SYN/ACK 包本身又有一个随机序号 B。
3. 最后，客户端再发送一个ACK。当服务端受到这个ACK的时候，就完成了三路握手，并进入了连接创建状态。此时包序号被设定为收到的确认号 A+1，而响应则为 B+1。

## 2 四次挥手

_注意: 中断连接端可以是客户端，也可以是服务器端. 下面仅以客户端断开连接举例, 反之亦然._

1. 客户端发送一个数据分段, 其中的 FIN 标记设置为1. 客户端进入 FIN-WAIT 状态. 该状态下客户端只接收数据, 不再发送数据.
2. 服务器接收到带有 FIN = 1 的数据分段, 发送带有 ACK = 1 的剩余数据分段, 确认收到客户端发来的 FIN 信息.
3. 服务器等到所有数据传输结束, 向客户端发送一个带有 FIN = 1 的数据分段, 并进入 CLOSE-WAIT 状态, 等待客户端发来带有 ACK = 1 的确认报文.
4. 客户端收到服务器发来带有 FIN = 1 的报文, 返回 ACK = 1 的报文确认, 为了防止服务器端未收到需要重发, 进入 TIME-WAIT 状态. 服务器接收到报文后关闭连接. 客户端等待 2MSL 后未收到回复, 则认为服务器成功关闭, 客户端关闭连接.

图解: http://blog.csdn.net/whuslei/article/details/6667471

## 3 ARP协议

地址解析协议(Address Resolution Protocol)，其基本功能为透过目标设备的IP地址，查询目标的MAC地址，以保证通信的顺利进行。它是IPv4网络层必不可少的协议，不过在IPv6中已不再适用，并被邻居发现协议（NDP）所替代。

## 4 urllib和urllib2的区别

这个面试官确实问过,当时答的urllib2可以Post而urllib不可以.

1. urllib提供urlencode方法用来GET查询字符串的产生，而urllib2没有。这是为何urllib常和urllib2一起使用的原因。
2. urllib2可以接受一个Request类的实例来设置URL请求的headers，urllib仅可以接受URL。这意味着，你不可以伪装你的User Agent字符串等。


## 5 Post和Get
[GET和POST有什么区别？及为什么网上的多数答案都是错的](http://www.cnblogs.com/nankezhishi/archive/2012/06/09/getandpost.html)
[知乎回答](https://www.zhihu.com/question/31640769?rf=37401322)

get: [RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1](http://tools.ietf.org/html/rfc2616#section-9.3)
post: [RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1](http://tools.ietf.org/html/rfc2616#section-9.5)



## 6 Cookie和Session

|      | Cookie                     | Session |
| :--- | :------------------------- | :------ |
| 储存位置 | 客户端                        | 服务器端    |
| 目的   | 跟踪会话，也可以保存用户偏好设置或者保存用户名密码等 | 跟踪会话    |
| 安全性  | 不安全                        | 安全      |

session技术是要使用到cookie的，之所以出现session技术，主要是为了安全。

web开发发展至今，`cookie`和`session`的使用已经出现了一些非常成熟的方案。在如今的市场或者企业里，一般有两种存储方式：

- 存储在服务端：通过`cookie`存储一个`sessionid`，然后具体的数据则是保存在`session`中。如果用户已经登录，则服务器会在`cookie`中保存一个`sessionid`，下次再次请求的时候，会把该`sessionid`携带上来，服务器根据`sessionid`在session库中获取用户的session数据。就能知道该用户到底是谁，以及之前保存的一些状态信息。这种专业术语叫做server side session。Django把`session`信息默认存储到数据库中，当然也可以存储到其他地方，比如缓存中，文件系统中等。存储在服务器的数据会更加的安全，不容易被窃取。但存储在服务器也有一定的弊端，就是会占用服务器的资源，但现在服务器已经发展至今，一些`session`信息还是绰绰有余的。
- 将`session`数据加密，然后存储在`cookie`中。这种专业术语叫做`client side session`。`flask`框架默认采用的就是这种方式，但是也可以替换成其他形式。

## 7 apache和nginx的区别

nginx 相对 apache 的优点：
* 轻量级，同样起web 服务，比apache 占用更少的内存及资源
* 抗并发，nginx 处理请求是异步非阻塞的，支持更多的并发连接，而apache 则是阻塞型的，在高并发下nginx 能保持低资源低消耗高性能
* 配置简洁
* 高度模块化的设计，编写模块相对简单
* 社区活跃

apache 相对nginx 的优点：
* rewrite ，比nginx 的rewrite 强大
* 模块超多，基本想到的都可以找到
* 少bug ，nginx 的bug 相对较多
* 超稳定

## 8 网站用户密码保存

1. 明文保存
2. 明文hash后保存,如md5
3. MD5+Salt方式,这个salt可以随机
4. 知乎使用了Bcrypy(好像)加密

## 9 HTTP和HTTPS


| 状态码       | 定义               |
| :-------- | :--------------- |
| 1xx 报告    | 接收到请求，继续进程       |
| 2xx 成功    | 步骤成功接收，被理解，并被接受  |
| 3xx 重定向   | 为了完成请求,必须采取进一步措施 |
| 4xx 客户端出错 | 请求包括错的顺序或不能完成    |
| 5xx 服务器出错 | 服务器无法完成显然有效的请求   |

403: Forbidden
404: Not Found

HTTPS握手,对称加密,非对称加密,TLS/SSL,RSA

## 10 XSRF和XSS

* CSRF(Cross-site request forgery)跨站请求伪造
* XSS(Cross Site Scripting)跨站脚本攻击

CSRF重点在请求,XSS重点在脚本

## 11 幂等 Idempotence

HTTP方法的幂等性是指一次和多次请求某一个资源应该具有同样的**副作用**。(注意是副作用)

`GET http://www.bank.com/account/123456`，不会改变资源的状态，不论调用一次还是N次都没有副作用。请注意，这里强调的是一次和N次具有相同的副作用，而不是每次GET的结果相同。`GET http://www.news.com/latest-news`这个HTTP请求可能会每次得到不同的结果，但它本身并没有产生任何副作用，因而是满足幂等性的。

DELETE方法用于删除资源，有副作用，但它应该满足幂等性。比如：`DELETE http://www.forum.com/article/4231`，调用一次和N次对系统产生的副作用是相同的，即删掉id为4231的帖子；因此，调用者可以多次调用或刷新页面而不必担心引起错误。


POST所对应的URI并非创建的资源本身，而是资源的接收者。比如：`POST http://www.forum.com/articles`的语义是在`http://www.forum.com/articles`下创建一篇帖子，HTTP响应中应包含帖子的创建状态以及帖子的URI。两次相同的POST请求会在服务器端创建两份资源，它们具有不同的URI；所以，POST方法不具备幂等性。

PUT所对应的URI是要创建或更新的资源本身。比如：`PUT http://www.forum/articles/4231`的语义是创建或更新ID为4231的帖子。对同一URI进行多次PUT的副作用和一次PUT是相同的；因此，PUT方法具有幂等性。


## 12 RESTful架构(SOAP,RPC)

推荐: http://www.ruanyifeng.com/blog/2011/09/restful.html


## 13 SOAP

SOAP（原为Simple Object Access Protocol的首字母缩写，即简单对象访问协议）是交换数据的一种协议规范，使用在计算机网络Web服务（web service）中，交换带结构信息。SOAP为了简化网页服务器（Web Server）从XML数据库中提取数据时，节省去格式化页面时间，以及不同应用程序之间按照HTTP通信协议，遵从XML格式执行资料互换，使其抽象于语言实现、平台和硬件。

## 14 RPC

RPC（Remote Procedure Call Protocol）——远程过程调用协议，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。RPC协议假定某些传输协议的存在，如TCP或UDP，为通信程序之间携带信息数据。在OSI网络通信模型中，RPC跨越了传输层和应用层。RPC使得开发包括网络分布式多程序在内的应用程序更加容易。

总结:服务提供的两大流派.传统意义以方法调用为导向通称RPC。为了企业SOA,若干厂商联合推出webservice,制定了wsdl接口定义,传输soap.当互联网时代,臃肿SOA被简化为http+xml/json.但是简化出现各种混乱。以资源为导向,任何操作无非是对资源的增删改查，于是统一的REST出现了.

进化的顺序: RPC -> SOAP -> RESTful

## 15 CGI和WSGI
CGI是通用网关接口，是连接web服务器和应用程序的接口，用户通过CGI来获取动态数据或文件等。
CGI程序是一个独立的程序，它可以用几乎所有语言来写，包括perl，c，lua，python等等。

WSGI, Web Server Gateway Interface，是Python应用程序或框架和Web服务器之间的一种接口，WSGI的其中一个目的就是让用户可以用统一的语言(Python)编写前后端。

官方说明：[PEP-3333](https://www.python.org/dev/peps/pep-3333/)

## 16 中间人攻击

在GFW里屡见不鲜的,呵呵.

中间人攻击（Man-in-the-middle attack，通常缩写为MITM）是指攻击者与通讯的两端分别创建独立的联系，并交换其所收到的数据，使通讯的两端认为他们正在通过一个私密的连接与对方直接对话，但事实上整个会话都被攻击者完全控制。

## 17 c10k问题

所谓c10k问题，指的是服务器同时支持成千上万个客户端的问题，也就是concurrent 10 000 connection（这也是c10k这个名字的由来）。
推荐: https://my.oschina.net/xianggao/blog/664275

## 18 socket

推荐: http://www.360doc.com/content/11/0609/15/5482098_122692444.shtml

Socket=Ip address+ TCP/UDP + port

## 19 浏览器缓存

推荐: http://www.cnblogs.com/skynet/archive/2012/11/28/2792503.html

304 Not Modified

## 20 HTTP1.0和HTTP1.1

推荐: http://blog.csdn.net/elifefly/article/details/3964766

1. 请求头Host字段,一个服务器多个网站
2. 长链接
3. 文件断点续传
4. 身份认证,状态管理,Cache缓存

HTTP请求8种方法介绍 
HTTP/1.1协议中共定义了8种HTTP请求方法，HTTP请求方法也被叫做“请求动作”，不同的方法规定了不同的操作指定的资源方式。服务端也会根据不同的请求方法做不同的响应。

GET

GET请求会显示请求指定的资源。一般来说GET方法应该只用于数据的读取，而不应当用于会产生副作用的非幂等的操作中。

GET会方法请求指定的页面信息，并返回响应主体，GET被认为是不安全的方法，因为GET方法会被网络蜘蛛等任意的访问。

HEAD

HEAD方法与GET方法一样，都是向服务器发出指定资源的请求。但是，服务器在响应HEAD请求时不会回传资源的内容部分，即：响应主体。这样，我们可以不传输全部内容的情况下，就可以获取服务器的响应头信息。HEAD方法常被用于客户端查看服务器的性能。

POST

POST请求会 向指定资源提交数据，请求服务器进行处理，如：表单数据提交、文件上传等，请求数据会被包含在请求体中。POST方法是非幂等的方法，因为这个请求可能会创建新的资源或/和修改现有资源。

PUT

PUT请求会身向指定资源位置上传其最新内容，PUT方法是幂等的方法。通过该方法客户端可以将指定资源的最新数据传送给服务器取代指定的资源的内容。

DELETE

DELETE请求用于请求服务器删除所请求URI（统一资源标识符，Uniform Resource Identifier）所标识的资源。DELETE请求后指定资源会被删除，DELETE方法也是幂等的。

CONNECT

CONNECT方法是HTTP/1.1协议预留的，能够将连接改为管道方式的代理服务器。通常用于SSL加密服务器的链接与非加密的HTTP代理服务器的通信。

OPTIONS

OPTIONS请求与HEAD类似，一般也是用于客户端查看服务器的性能。 这个方法会请求服务器返回该资源所支持的所有HTTP请求方法，该方法会用’*’来代替资源名称，向服务器发送OPTIONS请求，可以测试服务器功能是否正常。JavaScript的XMLHttpRequest对象进行CORS跨域资源共享时，就是使用OPTIONS方法发送嗅探请求，以判断是否有对指定资源的访问权限。 允许

TRACE

TRACE请求服务器回显其收到的请求信息，该方法主要用于HTTP请求的测试或诊断。

HTTP/1.1之后增加的方法

在HTTP/1.1标准制定之后，又陆续扩展了一些方法。其中使用中较多的是 PATCH 方法：

PATCH

PATCH方法出现的较晚，它在2010年的RFC 5789标准中被定义。PATCH请求与PUT请求类似，同样用于资源的更新。二者有以下两点不同：

但PATCH一般用于资源的部分更新，而PUT一般用于资源的整体更新。 
当资源不存在时，PATCH会创建一个新的资源，而PUT只会对已在资源进行更新。

## 21 Ajax
AJAX,Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）, 是与在不重新加载整个页面的情况下，与服务器交换数据并更新部分网页的技术。

# *NIX

## unix进程间通信方式(IPC)

1. 管道（Pipe）：管道可用于具有亲缘关系进程间的通信，允许一个进程和另一个与它有共同祖先的进程之间进行通信。
2. 命名管道（named pipe）：命名管道克服了管道没有名字的限制，因此，除具有管道所具有的功能外，它还允许无亲缘关系进程间的通信。命名管道在文件系统中有对应的文件名。命名管道通过命令mkfifo或系统调用mkfifo来创建。
3. 信号（Signal）：信号是比较复杂的通信方式，用于通知接受进程有某种事件发生，除了用于进程间通信外，进程还可以发送信号给进程本身；linux除了支持Unix早期信号语义函数sigal外，还支持语义符合Posix.1标准的信号函数sigaction（实际上，该函数是基于BSD的，BSD为了实现可靠信号机制，又能够统一对外接口，用sigaction函数重新实现了signal函数）。
4. 消息（Message）队列：消息队列是消息的链接表，包括Posix消息队列system V消息队列。有足够权限的进程可以向队列中添加消息，被赋予读权限的进程则可以读走队列中的消息。消息队列克服了信号承载信息量少，管道只能承载无格式字节流以及缓冲区大小受限等缺
5. 共享内存：使得多个进程可以访问同一块内存空间，是最快的可用IPC形式。是针对其他通信机制运行效率较低而设计的。往往与其它通信机制，如信号量结合使用，来达到进程间的同步及互斥。
6. 内存映射（mapped memory）：内存映射允许任何多个进程间通信，每一个使用该机制的进程通过把一个共享的文件映射到自己的进程地址空间来实现它。
7. 信号量（semaphore）：主要作为进程间以及同一进程不同线程之间的同步手段。
8. 套接口（Socket）：更为一般的进程间通信机制，可用于不同机器之间的进程间通信。起初是由Unix系统的BSD分支开发出来的，但现在一般可以移植到其它类Unix系统上：Linux和System V的变种都支持套接字。


# 数据结构

## 1 红黑树

红黑树与AVL的比较：

AVL是严格平衡树，因此在增加或者删除节点的时候，根据不同情况，旋转的次数比红黑树要多；

红黑是用非严格的平衡来换取增删节点时候旋转次数的降低；

所以简单说，如果你的应用中，搜索的次数远远大于插入和删除，那么选择AVL，如果搜索，插入删除次数几乎差不多，应该选择RB。

红黑树详解: https://xieguanglei.github.io/blog/post/red-black-tree.html

教你透彻了解红黑树: https://github.com/julycoding/The-Art-Of-Programming-By-July/blob/master/ebook/zh/03.01.md

# 编程题

## 1 台阶问题/斐波那契

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```python
fib = lambda n: n if n <= 2 else fib(n - 1) + fib(n - 2)
```

第二种记忆方法

```python
def memo(func):
    cache = {}
    def wrap(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrap


@memo
def fib(i):
    if i < 2:
        return 1
    return fib(i-1) + fib(i-2)
```

第三种方法

```python
def fib(n):
    a, b = 0, 1
    for _ in xrange(n):
        a, b = b, a + b
    return b
```

## 2 变态台阶问题

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

```python
fib = lambda n: n if n < 2 else 2 * fib(n - 1)
```

## 3 矩形覆盖

我们可以用`2*1`的小矩形横着或者竖着去覆盖更大的矩形。请问用n个`2*1`的小矩形无重叠地覆盖一个`2*n`的大矩形，总共有多少种方法？

>第`2*n`个矩形的覆盖方法等于第`2*(n-1)`加上第`2*(n-2)`的方法。

```python
f = lambda n: 1 if n < 2 else f(n - 1) + f(n - 2)
```

## 4 杨氏矩阵查找

在一个m行n列二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

使用Step-wise线性搜索。

```python
def get_value(l, r, c):
    return l[r][c]

def find(l, x):
    m = len(l) - 1
    n = len(l[0]) - 1
    r = 0
    c = n
    while c >= 0 and r <= m:
        value = get_value(l, r, c)
        if value == x:
            return True
        elif value > x:
            c = c - 1
        elif value < x:
            r = r + 1
    return False
```

## 5 去除列表中的重复元素

用集合

```python
list(set(l))
```

用字典

```python
l1 = ['b','c','d','b','c','a','a']
l2 = {}.fromkeys(l1).keys()
print l2
```

用字典并保持顺序

```python
l1 = ['b','c','d','b','c','a','a']
l2 = list(set(l1))
l2.sort(key=l1.index)
print l2
```

列表推导式

```python
l1 = ['b','c','d','b','c','a','a']
l2 = []
[l2.append(i) for i in l1 if not i in l2]
```

sorted排序并且用列表推导式.

l = ['b','c','d','b','c','a','a']
[single.append(i) for i in sorted(l) if i not in single]
print single

## 6 链表成对调换

`1->2->3->4`转换成`2->1->4->3`.

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    # @param a ListNode
    # @return a ListNode
    def swapPairs(self, head):
        if head != None and head.next != None:
            next = head.next
            head.next = self.swapPairs(next.next)
            next.next = head
            return next
        return head
```

## 7 创建字典的方法

### 1 直接创建

```python
dict = {'name':'earth', 'port':'80'}
```

### 2 工厂方法

```python
items=[('name','earth'),('port','80')]
dict2=dict(items)
dict1=dict((['name','earth'],['port','80']))
```

### 3 fromkeys()方法

```python
dict1={}.fromkeys(('x','y'),-1)
dict={'x':-1,'y':-1}
dict2={}.fromkeys(('x','y'))
dict2={'x':None, 'y':None}
```

## 8 合并两个有序列表

知乎远程面试要求编程

>  尾递归

```python
def _recursion_merge_sort2(l1, l2, tmp):
    if len(l1) == 0 or len(l2) == 0:
        tmp.extend(l1)
        tmp.extend(l2)
        return tmp
    else:
        if l1[0] < l2[0]:
            tmp.append(l1[0])
            del l1[0]
        else:
            tmp.append(l2[0])
            del l2[0]
        return _recursion_merge_sort2(l1, l2, tmp)

def recursion_merge_sort2(l1, l2):
    return _recursion_merge_sort2(l1, l2, [])
```

>  循环算法

思路：

定义一个新的空列表

比较两个列表的首个元素

小的就插入到新列表里

把已经插入新列表的元素从旧列表删除

直到两个旧列表有一个为空

再把旧列表加到新列表后面


```pyhton
def loop_merge_sort(l1, l2):
    tmp = []
    while len(l1) > 0 and len(l2) > 0:
        if l1[0] < l2[0]:
            tmp.append(l1[0])
            del l1[0]
        else:
            tmp.append(l2[0])
            del l2[0]
    tmp.extend(l1)
    tmp.extend(l2)
    return tmp
```


> pop弹出

```Python
a = [1,2,3,7]
b = [3,4,5]

def merge_sortedlist(a,b):
    c = []
    while a and b:
        if a[0] >= b[0]:
            c.append(b.pop(0))
        else:
            c.append(a.pop(0))
    while a:
        c.append(a.pop(0))
    while b:
        c.append(b.pop(0))
    return c
print merge_sortedlist(a,b)
    
```


## 9 交叉链表求交点

> 其实思想可以按照从尾开始比较两个链表，如果相交，则从尾开始必然一致，只要从尾开始比较，直至不一致的地方即为交叉点，如图所示

![](http://hi.csdn.net/attachment/201106/28/0_1309244136MWLP.gif)

```python
# 使用a,b两个list来模拟链表，可以看出交叉点是 7这个节点
a = [1,2,3,7,9,1,5]
b = [4,5,7,9,1,5]

for i in range(1,min(len(a),len(b))):
    if i==1 and (a[-1] != b[-1]):
        print "No"
        break
    else:
        if a[-i] != b[-i]:
            print "交叉节点：",a[-i+1]
            break
        else:
            pass
```

> 另外一种比较正规的方法，构造链表类

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
def node(l1, l2):
    length1, lenth2 = 0, 0
    # 求两个链表长度
    while l1.next:
        l1 = l1.next
        length1 += 1
    while l2.next:
        l2 = l2.next
        length2 += 1
    # 长的链表先走
    if length1 > lenth2:
        for _ in range(length1 - length2):
            l1 = l1.next
    else:
        for _ in range(length2 - length1):
            l2 = l2.next
    while l1 and l2:
        if l1.next == l2.next:
            return l1.next
        else:
            l1 = l1.next
            l2 = l2.next
```

修改了一下:


```python
#coding:utf-8
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

def node(l1, l2):
    length1, length2 = 0, 0
    # 求两个链表长度
    while l1.next:
        l1 = l1.next#尾节点
        length1 += 1
    while l2.next:
        l2 = l2.next#尾节点
        length2 += 1

    #如果相交
    if l1.next == l2.next:
        # 长的链表先走
        if length1 > length2:
            for _ in range(length1 - length2):
                l1 = l1.next
            return l1#返回交点
        else:
            for _ in range(length2 - length1):
                l2 = l2.next
            return l2#返回交点
    # 如果不相交
    else:
        return
```


思路: http://humaoli.blog.163.com/blog/static/13346651820141125102125995/


## 10 二分查找


```python

#coding:utf-8
def binary_search(list, item):
    low = 0
    high = len(list) - 1
    while low <= high:
        mid = (high - low) / 2 + low    # 避免(high + low) / 2溢出
        guess = list[mid]
        if guess > item:
            high = mid - 1
        elif guess < item:
            low = mid + 1
        else:
            return mid
    return None
mylist = [1,3,5,7,9]
print binary_search(mylist, 3)

```

参考: http://blog.csdn.net/u013205877/article/details/76411718

## 11 快排

```python
#coding:utf-8
def quicksort(list):
    if len(list)<2:
        return list
    else:
        midpivot = list[0]
        lessbeforemidpivot = [i for i in list[1:] if i<=midpivot]
        biggerafterpivot = [i for i in list[1:] if i > midpivot]
        finallylist = quicksort(lessbeforemidpivot)+[midpivot]+quicksort(biggerafterpivot)
        return finallylist

print quicksort([2,4,6,7,1,2,5])
```


>  更多排序问题可见：[数据结构与算法-排序篇-Python描述](http://blog.csdn.net/mrlevo520/article/details/77829204)


## 12 找零问题


```python

#coding:utf-8
#values是硬币的面值values = [ 25, 21, 10, 5, 1]
#valuesCounts   钱币对应的种类数
#money  找出来的总钱数
#coinsUsed   对应于目前钱币总数i所使用的硬币数目

def coinChange(values,valuesCounts,money,coinsUsed):
    #遍历出从1到money所有的钱数可能
    for cents in range(1,money+1):
        minCoins = cents
        #把所有的硬币面值遍历出来和钱数做对比
        for kind in range(0,valuesCounts):
            if (values[kind] <= cents):
                temp = coinsUsed[cents - values[kind]] +1
                if (temp < minCoins):
                    minCoins = temp
        coinsUsed[cents] = minCoins
        print ('面值:{0}的最少硬币使用数为:{1}'.format(cents, coinsUsed[cents]))

```

思路: http://blog.csdn.net/wdxin1322/article/details/9501163

方法: http://www.cnblogs.com/ChenxofHit/archive/2011/03/18/1988431.html

## 13 广度遍历和深度遍历二叉树

给定一个数组，构建二叉树，并且按层次打印这个二叉树


## 14 二叉树节点

```python

class Node(object):
    def __init__(self, data, left=None, right=None):
        self.data = data
        self.left = left
        self.right = right

tree = Node(1, Node(3, Node(7, Node(0)), Node(6)), Node(2, Node(5), Node(4)))

```

## 15 层次遍历

```python

def lookup(root):
    row = [root]
    while row:
        print(row)
        row = [kid for item in row for kid in (item.left, item.right) if kid]

```

## 16 深度遍历

```python

def deep(root):
    if not root:
        return
    print root.data
    deep(root.left)
    deep(root.right)

if __name__ == '__main__':
    lookup(tree)
    deep(tree)
```

## 17 前中后序遍历

深度遍历改变顺序就OK了

```python

#coding:utf-8
#二叉树的遍历
#简单的二叉树节点类
class Node(object):
    def __init__(self,value,left,right):
        self.value = value
        self.left = left
        self.right = right

#中序遍历:遍历左子树,访问当前节点,遍历右子树

def mid_travelsal(root):
    if root.left is not None:
        mid_travelsal(root.left)
    #访问当前节点
    print(root.value)
    if root.right is not None:
        mid_travelsal(root.right)

#前序遍历:访问当前节点,遍历左子树,遍历右子树

def pre_travelsal(root):
    print (root.value)
    if root.left is not None:
        pre_travelsal(root.left)
    if root.right is not None:
        pre_travelsal(root.right)

#后续遍历:遍历左子树,遍历右子树,访问当前节点

def post_trvelsal(root):
    if root.left is not None:
        post_trvelsal(root.left)
    if root.right is not None:
        post_trvelsal(root.right)
    print (root.value)

```

## 18 求最大树深

```python
def maxDepth(root):
        if not root:
            return 0
        return max(maxDepth(root.left), maxDepth(root.right)) + 1
```

## 19 求两棵树是否相同

```python
def isSameTree(p, q):
    if p == None and q == None:
        return True
    elif p and q :
        return p.val == q.val and isSameTree(p.left,q.left) and isSameTree(p.right,q.right)
    else :
        return False
```

## 20 前序中序求后序

推荐: http://blog.csdn.net/hinyunsin/article/details/6315502

```python
def rebuild(pre, center):
    if not pre:
        return
    cur = Node(pre[0])
    index = center.index(pre[0])
    cur.left = rebuild(pre[1:index + 1], center[:index])
    cur.right = rebuild(pre[index + 1:], center[index + 1:])
    return cur

def deep(root):
    if not root:
        return
    deep(root.left)
    deep(root.right)
    print root.data
```

## 21 单链表逆置

```python
class Node(object):
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

link = Node(1, Node(2, Node(3, Node(4, Node(5, Node(6, Node(7, Node(8, Node(9)))))))))

def rev(link):
    pre = link
    cur = link.next
    pre.next = None
    while cur:
        tmp = cur.next
        cur.next = pre
        pre = cur
        cur = tmp
    return pre

root = rev(link)
while root:
    print root.data
    root = root.next
```

思路: http://blog.csdn.net/feliciafay/article/details/6841115

方法: http://www.xuebuyuan.com/2066385.html?mobile=1


## 22 两个字符串是否是变位词

```python
class Anagram:
    """
    @:param s1: The first string
    @:param s2: The second string
    @:return true or false
    """
    def Solution1(s1,s2):
        alist = list(s2)

        pos1 = 0
        stillOK = True

        while pos1 < len(s1) and stillOK:
            pos2 = 0
            found = False
            while pos2 < len(alist) and not found:
                if s1[pos1] == alist[pos2]:
                    found = True
                else:
                    pos2 = pos2 + 1

            if found:
                alist[pos2] = None
            else:
                stillOK = False

            pos1 = pos1 + 1

        return stillOK

    print(Solution1('abcd','dcba'))

    def Solution2(s1,s2):
        alist1 = list(s1)
        alist2 = list(s2)

        alist1.sort()
        alist2.sort()


        pos = 0
        matches = True

        while pos < len(s1) and matches:
            if alist1[pos] == alist2[pos]:
                pos = pos + 1
            else:
                matches = False

        return matches

    print(Solution2('abcde','edcbg'))

    def Solution3(s1,s2):
        c1 = [0]*26
        c2 = [0]*26

        for i in range(len(s1)):
            pos = ord(s1[i])-ord('a')
            c1[pos] = c1[pos] + 1

        for i in range(len(s2)):
            pos = ord(s2[i])-ord('a')
            c2[pos] = c2[pos] + 1

        j = 0
        stillOK = True
        while j<26 and stillOK:
            if c1[j] == c2[j]:
                j = j + 1
            else:
                stillOK = False

        return stillOK

    print(Solution3('apple','pleap'))
```




## 23 动态规划问题

>  可参考：[动态规划(DP)的整理-Python描述](http://blog.csdn.net/mrlevo520/article/details/75676160)

