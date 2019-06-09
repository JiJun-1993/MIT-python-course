Day3
1、字符串函数：
前面我们讲了计算机输入输出操作的最小单位是字符。就是一个字母A或者一个数字1，或者一个其他的字符&等等。但是计算机输入输出设备可以一次性操作一连串字符。比如”sd34f+0的d”, 叫做字符串，今天我们要学习的是对字符串更加细致的操作，就是把字符串看做一个队列，这个队列的每一个位置都有自己编号，我们可以通过编号来操作这个队列，活脱脱就像是教官在训练队伍，而从现在开始，我们把字符串叫做字符数组
2、s[start : stop : step] 
其中的start ， stop， step 就是操作字符数组中某个或者某几个字符的下标，或者编号
不过，我们只能对字符数组做读取，不能做改变。
s1 = "mit u rock"
s2 = "i rule mit"
for i in s1:
    for j in s2:
        if i == j:
            print("common letter")
            break
这个例子的意思是找到s2和s1两个字符串中共有的字符。
看似是对if else的应用，其实是为了引出后面的穷举法找立方根。例子虽然简单，但是总这里可以看出来这个课程的巧妙，因为会一步一步将我们引向重点：排序和查找算法。
3、GUESS-AND-CHECK – cube root 
接着上面的例子，我们这里开始接触穷举法，就是最原始，最基础的查找算法。
cube = int(raw_input("please input a number as a cube:"))
for guess in  range(abs(cube) + 1):
    if guess**3  == abs(cube):
        break
if guess**3 != cube:
    print('%d is not a pefect cube'%cube)
else:
    if cube < 0:
        guess = -guess
    else:
        print('Cube root of'+str(cube)+' is ‘+str(guess))
我把原来的例子稍微改了一下, 允许用户自己输入cube。因为我用的是python2，所以输入函数有点不一样。然后是第6行，用了一个格式化输出
这个例子就是群举法解决问题的很好的例子
4 APPROXIMATE SOLUTIONS 
我们知道，大部分数是没法开整数立方根的，但是可以求一个近似解，比如误差在0.01范围内的一个解 
还是采用穷举法，找到这么一个数x，符合| x**3 -  cube |  < 0.01
……..
解释一下这个例子：
从0开始，每次递增0.0001，寻找这样一个数x
注意一下输出结果，num_guesses =', 29997，老师设置了一个计数器，为了让我们看到为了查找结果，进行了29997次计算。很麻烦对不对，接下来要引出更省事儿的方法，二分查找法，就是每次排除掉一半，只在另一半里查找。这里有个常识，就是给出一个数字区间[ a , b],  
if  (a + b ) / 2 的三次方小于 cube，那么cube的立方根一定在    (a + b ) / 2 到 b之间，若果小于，则在a 到 (a + b ) / 2之间

可以看到只循环只执行了14次，这在实际运行中就是绝对的省时省力，可见好的算法的重要性
5、回答下面的问题
允许用户输入的X < 1 如何应付
cube = float(input('a number'))
guess = 0.0
high = cube
low = 0
if cube < 1:
    low = cube
    high = 1
epsilon = 0.001
guess = (high + low) / 2.0
’’’注意这里分母上是2.0 不是2 ’’’
num_guesses = 0
while abs(guess**3 - cube) >= epsilon:
    if guess**3 < cube:
        low = guess
    else:
         high = guess
    guess = (high + low) / 2.0
    num_guesses += 1
print('num_guesses =', num_guesses)
print(guess, 'is close to the cube root of', cube)
