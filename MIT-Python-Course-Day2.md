1、一般的编程语言里有个标准函数库，叫做输入和输出，I/O，其背后的硬件基础就是第一讲：what is a computer 里面讲的计算机的组成当中的输入和输出设备
 关于字符串，这里给出一个通用定义：
一种常用的表示法是使用一个字符代码的数组，每个字符占用一个字节（如在ASCII代码中）或两个字节（如在unicode中）。它的长度可以使用一个结束符（一般是NUL，ASCII代码是0，在C编程语言中使用这种方法）。或者在前面加入一个整数值来表示它的长度（在Pascal语言中使用这种方法）。

总之就是编程语言处理输入输出的基本单位就是字符，而字符串是字符的一个集合，这就能理解为什么可以对字符串进行* 或者 + 的操作了

2、input , 是最基础的我们和计算机进行交互的方式，这里大家可以把这个input看做是广义的和计算机交互的方式，比如我们的刷脸支付，比如我们用的扫描仪等等。
3、学完了输入和输出，我们好像可以做一点简单的事儿了，比如写一个简单的计算器了，比如： 
a = int(input("first number"))
b = int(input("second number"))
print('a*b = %d’%(a*b))
但是它只能有一个相乘的功能，并且只能使用一次，是不能交付的。所以我们用动力，也有理由去改进一下，比如能不能在输入两个数后我们可以选择要进行的操作，比如打印出四种运算符，我们从中选一种。
如下：
a = int(input("first number"))
b = int(input("second number”))
print(“please select your operation: 1. +   2. —  3. * 、4 .  /  ”)
op = input()
然后，我们希望让特定的选择触发特定的流程，这就需要流程控制了：如果怎样那么就怎样
继续
if op == 1:
    print("a + b = ",a+b)
elif op == 2:   
    print("a - b = ",a-b)
elif op == 3:    
    print("a * b = ",a*b)   
elif op == 4:    
    print("a / b = ",a/b) 
这下完整了
但是只能用一次，用完就扔了，这个太太奢侈了，最好能无线复用
于是用到while
while 1：
	。。。。
省略处把上面的代码全部粘贴下来。 ok了，不过不完美，说是无限不能真的无限啊，不吃饭不睡觉了吗? 我们加个判断
m = 1
while m > 0:
	。。。。。  
  m = input("1: continue  0:exit")
有些情况下，我们要求算多少次之后就停止，比如
m = 1
while m > 10:
	。。。。。  
  m = m + 1
不过，编程语言里有另外一种专门用来应付这种要求固定次数的循环：for
for i in range(0,2):
    a = int(input("first number"))
    b = int(input("second number"))
    print("please select your operation:1: +、2: - 、3: * 、4: /")
    op = input()
    if op == 1:
        print("a + b = ",a+b)
    elif op == 2:   
        print("a - b = ",a-b)
    elif op == 3:    
        print("a * b = ",a*b)   
    elif op == 4:    
        print("a / b = ",a/b)
