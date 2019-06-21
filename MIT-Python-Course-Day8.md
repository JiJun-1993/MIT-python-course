Lecture 8: 面向对象编程

一、这是一种编程模式，就是面向对象的编程。
Python的每一种数据类型都是一种对象，
每一个对象都有一种类型
都有一种内部的数据表达，无论是初始的还是组合的。
有一组和这个对象交互的流程。
一个对象是一种类型的实例
. 12 是整形Int型的一个实例
.  “hello” 是字符串类型的一个实例

二、面向对象编程
python中的所有事物都是一个对象，并都有自己的一个类型
可以为一些类型创建新的对象
可以操作一个对象
可以销毁一个对象
	用del 或者只用 forget 来销毁
	有垃圾回收机制召回被销毁的或者无法访问的对象

三、什么是对象呢？
对象是一个数据抽象，包括
内部表示 通过数据属性
和对象交互的接口 通过方法，功能，流程 / 定义行为但是隐藏执行

四、internal representation 到底是什么意思
内部表示应该是私有的，不能被外界访问的
如果直接操作内部表示，正确的行为可能会被影响

五、面向对象的优势
将数据和通过合理定义的接口作用于这些数据的流程捆绑打包
分治法的发展
 	分别测试和实现每一个类的行为，强调类的独立性
	增加模块化，减少复杂度
类型让代码复用更容易
	许多Python的模块定义性新的类
	每一个类有独立的环境，当然，函数名不能有冲突。其实是强调每一个类都有独立的的存储和运行环境。
	继承机制允许子类重定义或者扩展父类的行为。

六、利用Class创建和使用你自己的类型
区分自己创建类和使用类的实例的区别
创建一个类
定义类名
定义类的属性
例如，有人会自己编写代码实现一个列表类
使用一个类，包括
创建一个类的新实例
对实例进行操作

七、什么是属性？

数据，可以把数据看做组成类型的其他类
方法：
？你可以定义两个坐标对象之间的距离，但是定义两个列表对象之间的距离就没意思了

八、关键，如何创建一个类

用__init__ 初始化这个类的数据

class Coordinate（object）:
	def _init_(self,x,y):
		self.x = y
		self.y = y

创建一个类的实例
c = Coordinate(3,4)
print(c.x)

还记得点运算吗？嘻嘻
一个实例的数据属性叫做实例变量，不要给属性提供叫self的属性

九、什么是方法
过程属性，专属于这一个类的方法
使用的惯例是吧self作为第一个变量，用“.” 运算访问任一一个变量，包括方法属性和数据属性

class Coordinate(object):
    def __init__(self, x, y):
self.x = x 
        self.y = y
    def distance(self, other):
这里有个奇怪的地方，在类的普通方法里面，必须要传递self代指任何类型，而其他语言会默认的self这个属性。

python有一个打印自己的信息的方法
_str_当然，你可以自己定义并重写这个方法

class Fraction(object):
    def __init__(self,numerator,denominator):
        self.denominator = denominator
        self.numerator = numerator
    def __add__(self,object):
        top  = self.numerator * object.denominator + self.denominator * object.numerator
        bott = self.denominator * object.denominator
        return top / bott
    def __float__(self):
        print 'hah'
        return float(self.numerator) / self.denominator
    def __str__(self):
        return str(self.numerator)+"/"+str(self.denominator)
    def inverse(self):
        return Fraction(self.denominator,self.numerator)
a = Fraction(3,4)
b = Fraction(1,3)
c = a + b 
print c #c是一个返回值的和，所以是一个整形值
print float(c) #c的浮点型结果
print float(a)
print (Fraction.__float__(a)) #调用Fraction的float函数，以Fraction的实例a做参数，返回a 的浮点型结果
print a #调用str 
print(float(a.inverse())) #返回一个新的Fraction对象
#其中比较难理解的是 print float(a) 和 print(float(a.inverse())) 只要是使用了float符号强制转换，
#就会调用实例对象的__float__函数

面向对象的威力
同一个bundle内共享
属性
操作这些属性的流程
用抽象去区分如何使用对象和如何实施对象
通过继承建立层级属性
创建python基础类的顶级类
Lecture8 习题

class Car(object):
	def __init__(self,w,d):
		self.w = w
		self.d = d
		self.color = “”
这里第三个self.color = “” 虽然init函数里面没有对应的形参，但是init函数在作用就是用来初始化变量的。注意这里的每一个关键字，self.color = “” self不能缺失，后面的“”更是要注意格式不能错
