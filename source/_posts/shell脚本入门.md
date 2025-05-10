---
title: shell脚本入门
date: 2025-02-06 19:13:24
tags:
        - Shell
        - 脚本
        - 运维
        - Linux

categories:
        - Shell
        - 脚本
        - 运维
        - Linux
---
# Shell脚本入门



## 常用命令

|  参考命令  |  |  |
| :---: | :---: | :---: |
| `cd` | `bash` | `vim` |
| `mkdir` | `ls` | `ps` |
| `top` | `lsof` | `|` |

---
## 流程控制
---
### if判断  

if语法中，句式以`if`开头以`fi`结尾。`if`后使用中括号来引用条件，中括号后使用英文分号   `;`结尾，并添加字符`then`承接下一步具体命令。转折使用`else`或者`elif`字符，可以引用多个`elif`添加判断。(中括号在shll中具有换行的作用)

<h4>单分支句式</h4>


---

```shell
if [条件判断式];then
	echo "output"  #执行的代码
else
	echo "outpu2"
fi
```

<h4>多分支句式</h4>

---
```shell
if [条件判断式];then
	echo "output"  #执行的代码
elif [条件判断式];then
	echo "output2" #执行的代码2
elif [条件判断式];then
	echo "output2" #执行的代码3
	..........
else
	echo "output#" #执行的代码
fi
```
### case 语句
---
使用case句式也可以完成多分支判断.
case语句使用case开头esac结尾，变量  in   另开一行加右括号，每次判断都要以两个英文冒号结尾。其中星号指的是“其他条件”，等同于if判断中的else，指的是其他的所有情况。

case语句示例

```shell
case $num in
1)
	echo "one"
;;
2)
	echo "two"
;;
*)
	echo "*"
;;
esac
```

### for循环
---
**`for`循环格式为：以`for`开头，后使用双层小括号或者使用中括来包裹初始条件，循环控制条件以及变量变化。随后在第二行添加字符`do`重起一行写执行的程序，最后以字符`done`结尾。（在条件的外围，我们更推荐使用双重小括号来进行包裹而不是中括号，是用中括号来进行包裹的时侯在中括号内部的两侧都要添加一个空格，在双重小括号中则不需要考虑留出空格，直接写条件即可）**

---
`（（sum +i））`**和**`[ $sum + $i ]`**是一样的效果**

---

```shell
for ((初始值;循环控制条件;变量变化))
do
	echo "output"  # 执行的代码
done
```
---
**案例一**

要求使用for循环来打印九九乘法表

```shell
#!/bin/bash
for ((i=1; i<=9; i++)); do
    for ((j=1; j<=i; j++)); do
        printf "%d×%d=%-2d " $j $i $((i*j))
    done
    echo
done
```
**输出**

```txt
root@ubuntu:~/shell/if# bash 2.sh 
1×1=1  
1×2=2  2×2=4  
1×3=3  2×3=6  3×3=9  
1×4=4  2×4=8  3×4=12 4×4=16 
1×5=5  2×5=10 3×5=15 4×5=20 5×5=25 
1×6=6  2×6=12 3×6=18 4×6=24 5×6=30 6×6=36 
1×7=7  2×7=14 3×7=21 4×7=28 5×7=35 6×7=42 7×7=49 
1×8=8  2×8=16 3×8=24 4×8=32 5×8=40 6×8=48 7×8=56 8×8=64 
1×9=9  2×9=18 3×9=27 4×9=36 5×9=45 6×9=54 7×9=63 8×9=72 9×9=81 
```

---
**案例二**

	题目：要求计算到用户输出数字的累加和
| 代码 1                                                       | 代码 2                                                       |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| #! /bin/bash<br> for ((i=1;i<=$1;i++))  <br/>  do <br/>  sum=$((sum + um))<br>  done<br>  echo $sum<br> | #！ /bin/bash <br> for ((i=1;i<=$1;i++) <br/> do <br/>   sum=$[ $num + $i ] <br> done <br/> echo $sum <br> |

**输出**

```bash
root@ubuntu:~/shell/if# bash 3.sh 100
5050
```

---
### while循环

while循环中使用while开头，后使用中括号（中括号内左右都要有一个空格）包裹判断式。随后使用do和done包裹执行的命令

---
**注意：在[]中只能使用比较符号，例如-le，-gt等。在(())中只能使用数学符号，<>+= 等符号**

---
```shell
while [ 条件判断式 ]
do
	#程序
done
```

---
**案例**

---
题目：使用while循环，计算1-100整数的累加和

```bash
#! /bin/bash
sum =0
i=1
while [ $i -le 100 ]  # while ((i<=100))
do
	sum=$[ $sum+$i ]  # let sum+=i
	i=$[ $i+1 ]       # let i++
done
echo $sum
```
### read读取命令

使用语法：                     ` read  (选项)  (参数)`  

例如 

```shell
read -t 6 -p "please input your answer"  answer  
# 读取输入的内容并将内容复制给`answer` 6秒无输入则退出执行
```
| 选项 | 释义 |
| ------ | ------ |
| -p | 读取输入的内容 |
| -t | 等待的时间(超时则执行会退出) |

---

## 函数

------
### 系统函数
---
* basename
* dirname

`basename` 用于打印当前文件的名字
`dirname`  用于打印当前文件的路径部分

### 自定义函数
---
基本语法
```shell
function function_name()
{
	Action
	return int; # 可要可不要
}
```
案例
题目:编写一个函数`add`，接受两个参数，并返回它们的和。

```bash
#！/bin/bash
function add()
{
	sum=$(($1+$2))
	echo "和为：$sum"
}
read -p "please input first num" num1
read -p "please input second num" num2
add $num1 $num2
```
```shell
root@ubuntu:~/shell/if# bash 5.sh 
please input first num3
please input secone num6
和为：9
```
题目：编写一个`factorial`函数，计算n的阶乘（n!）
```shell
#！/bin/bash
function factorial()
{
	n=$1
	result=1
	for ((i=1;i<=n;i++));
	do
		let result*=i    # ((result*=i))
	done
	echo $result

}
read -p "please input a number:" num
fact=$(factorial $num)
echo "n的阶乘为：$fact"
```
```txt
please input a number:4
n的阶乘为：24
```

### 归档文件

```shell
#! /bin/bash
if [ $# -ne 1 ];then
        echo "参数错误，应该输入一个参数"
        exit
fi

if [ -d $1 ];then
        echo
else
        echo "目录不存在"
        echo 
        exit
fi

DIR_NAME=$(basename $1)
DIR_PATH=$(cd $(dirname $1);pwd)

DATE=$(date +%y%m%d)

FILE=archive_${DIR_NAME}_$DATE.tar.gz
DEST=/root/archive/$FILE

echo "开始archive"
echo

tar -czf $DEST $DIR_PATH/$DIR_NAME

if [ $? -eq 0 ];then
        echo "archive successed!"
        echo "archive path is :$DEST"
else
        echo "archive fail"
fi
```
```shell
root@ubuntu:~/shell/if# bash 7.sh /root/shell/if

开始archive

tar: Removing leading `/' from member names
archive successed!
archive path is :/root/archive/archive_if_250205.tar.gz
root@ubuntu:~/shell/if# cd /root/archive/ && ll
total 12
drwxr-xr-x 2 root root 4096 Feb  5 15:49 ./
drwx------ 9 root root 4096 Feb  5 15:49 ../
-rw-r--r-- 1 root root 1042 Feb  5 15:49 archive_if_250205.tar.gz
```
### 正则表达式

<h4>使用特殊字符</h4>

* `^`   匹配一行的开头字母
```shell
	cat /root/shell/bash.sh | grep -n ^echo
	
	# 在文件bash.sh中匹配以echo字符开头的行，-n为列出所在的行号
```

* `$` 匹配一行的结束

```shell
	cat /root/shell/bash.sh | grep -n echo$
	
	# 在文件bash.sh中匹配以echo字符结尾的行，-n为列出所在的行号
```

* `.`匹配一个字符

```shell
	cat /root/shell/bash.sh | grep -n r..t
	
	# 在文件bash.sh中匹配含有r..t字符的行，-n为列出所在的行号
```

* `*` 匹配重复字符

```shell
	cat /root/shell/bash.sh | grep -n ro.t
	
	# 在文件bash.sh中匹配含有root字符或者rooot或者rooooot的行，-n为列出所在的行号
```
* `[]`匹配字符&范围
```shell
[a,b] [2,6]

#用于匹配列表中的字符
```
```shell
[1-9] 或 [a-z]
#用于匹配1-9或者a-z之间的一个字符
```
```shell
[1-9]* [a-z]*
#用于匹配范围内任意长度的字母或者字符串
```
```shell
[a-g,h-k]- 
#用于匹配a-g或者h-k间的任意字符
```

## 文本处理

`cut`

默认分隔符为制表符，也就是四个空格

---
基本用法

```shell
cut [选项参数] filename
```

---

| 选项参数 | 功能 |
| :------ | :------: |
| `-f` | 列号，提取第几列 |
| `-d` | 分隔符，按照指定分隔符分割列,默认分隔符为制表符`\t` |
| `-c` | 按字符进行切割，后加数字表示取第几列 |

---
***案例解析***
案例1：
```shell
cut -d " " -f 2  file_name.txt

使用`cut`命令，`-d` 指定分隔符为空格，`-f`指定截取的列数为第2列，截取自文件`file_name.txt`
```


案例二：
```bash
cut -d " " -f 2,3 file_name.txt
```
使用`cut`命令，`-d`指定分隔符为空格 `-f`指定截取的列数为第二第三列

---
案例三：
```bash
cat  /etc /passwd | grep bash$ | cut -d ":" -f 1,6,7
#执行结果如下
root@ubuntu:~/shell# cat /etc/passwd | grep bash$ | cut -d ":" -f 1,6,7
root:/root:/bin/bash
bing:/home/bing:/bin/bash
```
截取``/etc/passwd``目录下以``bash``结尾的行，并且只截取信息中以`:`作为分隔符隔开的内容，且只取第`1`、`6`、`7`三行的数据

案例四
```bash
echo $PATH | cut -d :"" -f 3-    #执行该代码
root@ubuntu:~/shell# echo $PATH   #打印原信息
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
root@ubuntu:~/shell# echo $PATH | cut -d :"" -f 3-    #通过命令对原信息截取
/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin    #截取后的信息
```

---
`awk`
基本用法：

```bash
awk 参数 ‘/条件/{执行的命令}’ 被处理的文件
```

| 参数 | 功能 |
| ----- | ----- |
| `-F` | 指定使用的分隔符 |
| `-v` | 赋值一个用户自定义变量 |

案例一
找出root用户工作的目录
```bash
cat /etc/passwd | grep ^root | cut -d ":" -f 7
# cat 和cut联合实现
# 输出
root@ubuntu:~/shell/if# cat /etc/passwd | grep ^root | cut -d ":" -f 7
/bin/bash
```
```shell
cat /etc/passwd | awk -F ":" '/^root/{print $7}'
# 使用cat和awk实现
#输出
root@ubuntu:~/shell/if# cat /etc/passwd | awk -F ":" '/^root/{print $7}'
/bin/bash
```

