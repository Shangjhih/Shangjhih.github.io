---
title: Python语法记录
date: 2025-02-09 22:32:37
tags:
    - python
    - 语法
categories: 
    - Python语法
---
# Python基础指南



#### 一 ：字符串的输入

**`input ('')`**

##### 例：

```python
input('please inout your name: \n')


#输出：

PS D:\Python\Python Project> & D:/Python/Python3.11.8/python.exe "d:/Python/Python <br>Project/main.py" 
 
please input your name: 	
```

-----

####  二：print输出并引用变量

##### 例：

- ##### 方法1：


```python
 name = 'shuqi'
 print('your name is %s' % name)


#输出：

PS D:\Python\Python Project> & D:/Python/Python3.11.8/python.exe "d:/Python/Python Project/main.py"

your name is shuqi
```

- ##### 方法2：
```python
name = 'shuqi'
print(f'your name is {str}')


#输出

PS D:\Python\Python Project> & D:/Python/Python3.11.8/python.exe "d:/Python/Python Project/main.py"

your name is shuqi	
```


-----
#### 注释

***行内注释***

> 使用# 作为一行的注释

***块注释***

\#和 前面的代码至少要相隔两个空格 ,#后必须空一格才能开始写注释

例如

```python
print ('hello word')   # 打印hello word
```

***多行注释***
使用```  ```作为多行注释符号


	print (多行注释)
	```
	这里是多行注释
	```
<h4>`print`拓展参数</h4>

print中每一部分的参数都要使用，逗号隔开，字符串使用单引号或双引号引起来

`sep="" 用于定义分隔符的形式

```python
year = 2027
print(year,"和律书琪结婚",sep="")
#输出
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\1.py 
2027年和律书琪结婚
```
***换行***

```py
print (end='\n')
```
`end=""`指的是在之前动作执行后继续执行的操作

```py
year = 2025
month =  2
day = 7
week = "tuesday"

weather = 'sunshine'
temperature = "-1"

	print("今天是", 'year', year, 'month', month, 'day', day, ',',
     	 "end=''", 'week', week, ',', "today's weather:", weather, ',', 		'temperature', temperature)
     # 这里是另一种写法
      print("today is year%d month%d day%d week%s, weather%s temperature%s"
      % (year, month, day, week, weather, temperature))
```
| 格式化字符 | 含义 |
| ------ | ------ |
| %s | 字符串 |
| %d | 有符号十进制数，%06d表示输出6位字符，不足低的方式用0补全 |
| %f | 浮点数，带小数。%.4f表示的是在小数点后保留4位小数 |
| %% | 输出% |

---
`input()`
<br>
***字符串转数字***

从input获取的输入信息都是字符串，即使是输入数字，从input接收后也会变成字符串。加入需要

将从input接收的数字作为实际的数字使用，可以使用以下代码进行转换


```py
age = input("please input your age:")

age= int(age)  # 使用int加括号来将字符串转换为数字

birth = 2025-age
print("your birth year is :", birth)
```
```py
# 运行结果
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-1-4-input.py 

please input your age:45

your birth year is : 1980
```

---
***变量赋值***

```py
# 多个变量值相等

num1 = num2 = num3 = 10
```
```py
# 多个变量的值不同，元组赋值

a, b = 10, 20
```

---
练习题：苹果的价格为10.5元每斤，买了7.5斤苹果，计算付款金额
```py
price = 10.5
weight = 7.5
money = price * weight
print()
print('您需要付款%d元' % money)   # print('您需要付款:', money, '元')
```

---
***数据类型***

| 类型 | 解释 | 例子 |
| ------ | ------ | ------ |
| 整型（integers） | 正数，不带小数点 | 100 |
| 浮点型（Floating point numbers） | 带有小数的数字 | 15.20 |
| 复数(Complex Numbers) | 带有实部和虚部的数字 | 3.14j |
| 布尔型(Boolean) | 表示真假 | 只有两个值，True、False |
| 字符串(String) | 一串字符 | ”Hello World！“ |
| 列表(List) | 有序的集合，可以包含任何数据类型 | [1,'a',2.3] |
| 元组(Tuple) | 类似于列表，但不可变 | (1,'a',2.3) |
| 集合(Set) | 无需且不重复的元素集合 | {1,2,3} |
| 字典(Dictionary) | 键值对的集合 | {'name':'john','age':30} |

四舍五入
```py
num1 = 1.23456
num2 = 3.23
n3= round(num1 + num2 , 2)
print()
print("your calculation result is:", n3)
# 运行结果
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

your calculation result is: 4.46
```
使用`round`函数进行四舍五入
```py
num1 = 1.23456
num2 = 3.23
n3= round(num1 + num2 , 2)    # 使用round函数保留两位小数
print()
print("your calculation result is:", n3)

# 执行结果
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

your calculation result is: 4.46
```

使用import调用math库对函数向上取整向下取整
```py
# 向上取整
num1 = 12.34
num2 = 3.12

import math                        # 此处使用import调用一次math库即可
n3 = math.ceil(num1 + num2)        # math.ceil（）为对括号内的算式向上取整
print(n3)

# 向下取整
num4 = math.floor(num1 + num2)     # math.floor（）为对括号内的算式向下取整
print(num4)

              ###### 执行结果#######
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 
16
15
```
<br>
<br>
***字符串***

使用双引号或单引号引起来的内容叫做 > >>>>>>`字符串`
```py
# 单引号字符串
str1 = 'hello'
print(str1)

# 双引号字符串
str2 = "Hello World!"
print(str2)

# 三引号字符串，多行字符串
str3 = '''Hello World, Hello 2026'''   # 使用三个单引号
str4 = """Hello World, Hello 2026"""   # 使用三个双引号
print(str3, str4, sep="\n")

                ########执行结果########

D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 
hello
Hello World!
Hello World, Hello 2026
Hello World, Hello 2026
```
<br>
<br>
***字符串运算***
字符串拼接
```py
str1 = 'python and shell '
str2 = 'are computer languages'
str = str1 + str2
print('拼接后的字符串为：', str)
                ########执行结果########
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

拼接后的字符串为： python and shell are computer languages
```

重复字符串


```py
str1 = 'language|'
str = str1 * 4
print(str)
                ########执行结果########
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

language|language|language|language|
```
<br>
<br>
***字符串的索引***


> 字符串的截取        str[位数]

> 字符串的切片        str[0:4] 加入范围 （***只截取第0到3位的字符***）

索引：从字符串中的任何一位或几位获取的单个字符，字符的顺序从0位开始

**备注：在中括号内使用负号来对字符进行排序就是倒着数第多少位，正着数有第0位，倒着数没有倒数第0位,字符串在切片取字符的时候可以使用[1:5:2],该代码对一个冒号并在最后加入了2，这表明在在第2个到第5个字符之间每隔两个字符取一个。**

```py
str1 = 'hello,world'
print('您选择的字符为：', str1[2], str1[6])  # 获取第三个和第七个字符
print('您选择的切片字符为：', str1[0:7])      # 使用切片获取第0到8个范围内的字符

                ########执行结果########
                
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

您选择的字符为： l w
您选择的切片字符为： hello,w
```
字符串顺序反转
```py
str1 = '123456789'
print(str1[::-1])
print(str1[-1:-10:-1])

                ########执行结果########
                
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

987654321
987654321
```

***数据类型的转换***

| 函数名 | 函数值 |
| ------ | ------ |
| int(x,[基数]) | 将数字或字符串转换为整数，如果x为浮点数，只保整数部分。基数用于转换进制，比如10代表十进制，2代表二进制 |
| float(x) | 转换为浮点型 |
| bool(x) | 转换为浮点型：True\False |
| str(x) | 转换为字符串，方便阅读 |
使用type命令来查看转换后变量的数据类型
例：int >>>>>bool
```py
s = 12
print(type(s))
print(type(bool(s)))

                ########执行结果########
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

<class 'int'>
<class 'bool'>
```
bool >>>>>> int
```py
n = True                   # 这里的True为布尔值
print(type(n))             # 这里检测n的数据类型
print(type(int(n)))        # 这里将布尔值转换为整型再检测数据类型

                ########执行结果########
D:\Python\Python3.13.2\python.exe E:\PythonProject\第1章\python-2-1-init.py 

<class 'bool'>
<class 'int'>

```


***算术运算符***

| 运算符 | 描述 | 实例 |
| ------ | ------ | ------ |
| + | 加 | 10+20=30 |
| - | 减 | 10-20=-10 |
|`*` | 乘 | 10\*20=200 |
| `/` | 除 | 20/10=2 |
| `//` | 取整 | 除法结果取整数部分 |
| `%`| 取余 | 除法结果部分取小数 |



***算数运算符的优先级***



| `**` | 幂 |
| ------ | ------ |
| `*/%//` | 乘，除，取余数，取整数 |
| `+ -` | 加法，减法 |



***赋值运算符***

| 运算符 | 描述 | 实例 |
| ------ | ------ | ------ |
| `=` | 赋值运算符 | c = a+b将a=b的运算结果复制为c |
| `+=` | 加法赋值运算符 | c += a等效于c = c+a |
| `-=` | 减法赋值运算符 | c-=a等效于c = c-a |
| `*=` | 乘法赋值运算符 | c*=a等效于c = c * a |
| `/=` | 除法赋值运算符 | c/=a等效于c = c/a |
| `//=` | 取整赋值运算符 | c//=a等效于c = c//a |
| `%=` | 取余赋值运算符 | c%=a等效于c = c%a |
| `**=` | 幂赋值运算符 | c\*\*=a等效于c = c \**a |

***比较运算符***

| 运算符 | 描述 |
| ------ | ------ |
| `==` | 检查两个操作数的值是否相等，如果是，则条件成立，返回True |
| `!=` | 检查两个操作数的值是否不相等，如果是，则条件成立，返回True |
| `>` | 检查左操作数的值是否大于右操作数的值，如果是,则条件成立，返回True |
| `<` | 检查左操作数的值是否小于右操作数的值，如果是,则条件成立，返回True |
| `>=` | 检查左操作数的值是否大于或等于右操作数的值，如果是,则条件成立，返回True |
| `<=` | 检查左操作数的值是否小于等于右操作数的值，如果是,则条件成立，返回True |

**逻辑运算符***

<br>
> 运算的优先级||||| not > and > or

<br>
| 运算符 | 逻辑表达式 | 描述 |
| ------ | ------ | ------- |
| `and` | x and y | 只有x和y的值都为True，才会返回True。否则只要x或者y有一个值为False，就会返回False |
| `or` | x or y | 只要x或者y有一个为True，就返回True，如果x和y都为False才会返回False |
| `not` | not x | 如果X为True，返回False。如果x为False，返回True |

***位运算符***

| 运算符 | 描述 | 功能 | 实例 |
| ------ | ------ | ------ | :------: |
| `&` | 与 | 参与运算的两个值，如果两个相应位都为1，则该位的结果为1否则为0 | 5&7 |
| `|` | 或 | 参与运算的两个值，如果两个相应位有一个为1时，则该位的结果为1，否则为0 | 5|7 |
| `^` | 异或 | 参与运算的两个时，如果两个相应位不同时，则该位的结果为1，否则为0 | 5^7 |
| `~` | 取反 | 对数据的每个二进位进行取反操作，把1变成0，把0变成1 | ~5 |
| `<<` | 左移 | 运算术的各二进制位全部向左移动若干位，若符号右侧的数字指定移动的位数，高位丢弃，低位补0 | 9<<2 |
| `>>` | 右移 | 运算术的各二进制位全部向右移动左边为，若符号右侧的数字指定移动的位数，低位丢弃，高位补丁 | 9>>2 |


***成员运算符***

| 运算符 | 描述 | 实例 |
| ------ | ------ | ------ |
| `in` | 如果在指定的序列中找到值返回True，否则返回False | 3 in (1,2,3) 返回True |
| `not in` |  如果在指定的序列中没有找到返回值返回True，否则返回False| 3 not in (1,2,3) 返回False |

***身份运算符***

| 运算符 | 描述 |
| ------ | ------ |
| `is` | 判断两个标识符是否引用同一个对象，是的话返回真，否则返回假 |
| `is not` | 判断两个标识符是否不是引用同一个对象，是的话返回真，否则返回假 |


***运算符的优先级***

|运算符  | 描述 |
| ------ | ------ |
| `**` |幂  |
| `~+-` | 按位取反，一元运算符 |
| `*/%//` | 乘、除、取整数、取余数 |
| `+-` | 加法、减法 |
| `<<>>` | 左移、右移 |
| `&` | 按位与 |
| ``` |^` |
| `>< >= <=` |比较运算符 |
| `== !=` | 等于运算符 |
|  `= += -= *= /= %= //= **=`| 赋值运算符 |
|  `is 、is not`|  |
|  `in 、not in`|  |
|  `not or and`| 逻辑运算符 |









### 条件判断

***if单分支***

```py
if 条件：     # if后直接写条件然后加英文冒号
    执行的命令         # 执行命令的部分要空四格再写命令作为执行命令
```
***if else 语句***

```py

if 判断条件：                   # if句后结尾加英文冒号
    条件成立执行的代码
else：                         # else后加英文冒号，和shell命令不同，要区分！！！！
    条件不成立执行的代码
```

***elif语句***

```py

if 判断条件:           # 注意此处的冒号
    执行的代码
elif 条件：             # 注意此处的冒号
    执行的代码
else:                  # 特别注意此处的冒号！！！！
    执行的代码
    
```
