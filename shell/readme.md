# shell 编程
## shell是一个命令行解释器，为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以使用shell来启动，挂起，停止甚至是编写一些程序。

·脚本要求格式

1. 脚本以#!/bin/bash开头

2. 脚本需要有可执行权限


·测试一个shell脚本

·执行方式

1. 给执行权限+x执行

2. sh+脚本执行

#!/bin/bash

echo "hello,world"
```
[root@fox01 shcode]# ./hello.sh
bash: ./hello.sh: 权限不够
[root@fox01 shcode]# chmod u+x hello.sh 
[root@fox01 shcode]# ./hello.sh 
hello,world
[root@fox01 shcode]# ll
总用量 4
-rwxr--r--. 1 root root 31  6月  3 17:38 hello.sh
[root@fox01 shcode]# ./hello.sh 
hello,world
[root@fox01 shcode]# chmod u-x hello.sh 
[root@fox01 shcode]# 
[root@fox01 shcode]# ll
总用量 4
-rw-r--r--. 1 root root 31  6月  3 17:38 hello.sh
[root@fox01 shcode]# 
[root@fox01 shcode]# sh hello.sh 
hello,world
```

## shell 变量
1. Linux Shell变量分为系统变量，用户自定义变量。

2. 系统变量如 $HOME, $PWD, $SHELL, $USER等。例echo $HOME等

3. 显示当前shell中所有变量 set

## 变量定义
1. 定义变量: 变量=值

2. 撤销变量: unset变量

3. 声明静态变量: readonly变量，不能unset

## 规则
1. 等号两边不能有空格

2. 变量名约定俗成大写

3. `date`将指令返回的结果赋值给变量
```
  1 #!/bin/bash
  2 # 案例1：定义变量A
  3 A=100
  4 #输出变量需要加$
  5 echo A=$A
  6 echo "A=$A"
  7 
  8 # 案例2：撤销变量A
  9 unset A
 10 echo A=$A
 11 
 12 # 案例3：声明静态变量B=2,不能unset
 13 readonly B=2
 14 echo B=$B
 15 unset B
 16 #./var.sh: 第 15 行：unset: B：无法取消设定: 只读 variable
 17 
 18 # 案例4：将指令返回的结果赋给变量
 19 C=`date`
 20 D=$(date)
 21 echo $C
 22 echo "D=$D"
```

## 设置环境变量

1. export变量名=变量值     将shell变量输出位环境变量/全局变量

2. source配置文件          让修改后的配置信息立即生效

3. echo $变量名            查询环境变量的值

shell多行注释 :<<! 内容 !

## 位置参数变量
```
#!/bin/bash
echo "0=$0 1=$1 2=$2"
echo "所有的参数=$*"
echo "$@"
echo "参数的个数=$#"

[root@fox01 shcode]# ./myshell.sh 100 200
0=./myshell.sh 1=100 2=200
所有的参数=100 200
100 200
参数的个数=2
```

## 预定义变量
·shell设计者事先定义好的变量，可以直接在shell脚本中使用

```
#!/bin/bash
echo "当前执行的进程id=$$"

# 以后台方式运行一个脚本，并获取他的进程号
/root/shcode/myshell.sh &
echo "最后一个后台方式运行的进程id=$!"
echo "执行的结果是=$?"

[root@fox01 shcode]# ./preVar.sh 
当前执行的进程id=74913
最后一个后台方式运行的进程id=74914
执行的结果是=0
0=/root/shcode/myshell.sh 1= 2=
所有的参数=

参数的个数=0

```

## 运算符
基本语法

1. “$((运算式))”或"$[运算式]"或者expr m + n

2. 注意expr运算符之间有空格,如果希望将expr结果赋给某个变量使用``

3. expr m - n

4. expr \*,/,% 乘除 取余
```
#!/bin/bash
# 计算（2+3）x4的结果
echo "(2+3)*4=$[(2+3)*4]"

# 求命令和两个参数整数的和
SUM=$[$1+$2]
echo "sum=$SUM"

[root@fox01 shcode]# ./operator.sh 20 70
(2+3)*4=20
sum=90
```

## 条件判断
[ condition ] (注意condition前后有空格)

#非空返回true，可用$?验证(0为true，>1为false)

[ hspEdu ]                                true
 
[]                                        false

[ condition ] && echo OK || echo notok    条件满足，执行后面的语句

·判断语句

1. = 字符串比较

2. 两个整数比较

   -lt 小于

   -le 小于等于

   -eq 等于

   -gt 大于

   -ge 大于等于

   -ne 不等于

3. 按照文件权限进行判断

-r 有读的权限；-w 有写的权限；-x 有执行的权限

4. 按照文件类型进行判断

-f 文件存在并且是一个常规文件

-e 文件存在

-d 文件存在病史一个目录
```
#!/bin/bash
# ok是否等于ok
if [ "ok" = "okk" ]
then
        echo "equal"
else
        echo "not equal"
fi

# 23是否大于等于22
if [ 23 -ge 22 ]
then
        echo "a>=b"
else
        echo "a<b"
fi

# /root/shcode/aaa.txt 目录中的文件是否存在
FILE=/root/shcode/aaa.txt
if [ -f $FILE ]
then
        echo "$FILE exist"
else
        echo "$FILE not exist"
fi
```

## 流程控制
if [condition]

then

code

fi

或者

if [condition]

then

code

elif [condition]

then

code

fi

注意事项：[条件片段式]，中括号和条件判断式之间必须有空格
```
#!/bin/bash
# 如果输入参数大于等于60,输出及格；如果小于60输出不及格
if [ $1 -ge 60 ]
then
        echo "及格"
elif [ $1 -lt 60 ]
then
        echo "不及格"
fi

```

## case
case $变量名 in
"值1")
如何变量的值等于1，则执行程序1
;;
"值2")
如何变量的值等于2，则执行程序2
;;
...省略其他分支...
*)
如果变量的值都不是以上的值，则执行程序此程序
;;
esac

```
#!/bin/bash
case $1 in
        "1")
                echo "monday"
                ;;
        "2")
                echo "tuesday"
                ;;
        *)
                echo "other"
                ;;
esac
```

## for
基本语法1

for 变量 in 值1 值2 值3...

do

程序

done
```
#!/bin/bash
# 打印命令行输入的参数， 这里可以看出$* $@的区别
# $*把输入的参数当作一个整体
for i in "$*"
do
        echo "num is $i"
done

for i in "$@"
do
        echo "num is $i"
done

[root@fox01 shcode]# ./forCase.sh 1 2 3 4 5
num is 1 2 3 4 5
num is 1
num is 2
num is 3
num is 4
num is 5
```

基本语法2

for ((初始值;循环控制条件;变量变化))

do

程序

done
```
#!/bin/bash
# 1-100输出显示
SUM=0
for (( i=1; i <= 100; i++ ))
do
        SUM=$[ $SUM+$i ]
        echo "sum=$SUM"
done
echo "$SUM"
```

## while
while [ condition ]

do

code

done

```
#!/bin/bash
# 命令行输入一个数n，统计1--n的和
SUM=0
i=1
while [ $i -le $1 ]
do
        SUM=$[ $SUM+$i ]
        i=$[ $i+1]
done
echo "$SUM"
```

## read读取控制台输入
read(选项)(参数)

选项：

-p: 指定读取值时的提示符；

-t: 指定读取值时等待的时间s，如果没有在指定时间输入，不再等待

参数:

变量: 指定读取值的变量名
```
#!/bin/bash
# 读取控制台输入的一个数值
read -p "Please enter N1=" N1
echo "N1=$N1"

# 读取输入一个数值，在10s内
read -t 10 -p "Please enter N2=" N2
echo "N2=$N2"
```

## 函数介绍
系统函数

basename基本语法

功能：返回完整路径最后/的部分，常用于获取文件名

basename [pathname][suffix]

basename [string][suffix]

选项：

suffix为后缀，如果suffix被指定，basename会将pathname或string中的suffix去掉
```
[root@fox01 shcode]# basename /home/aaa/test.txt
test.txt
[root@fox01 shcode]# basename /home/aaa/test.txt  .txt
test
```

dirname基本语法

功能：返回完整路径最后/的前面部分，常用于返回路径部分

dirname文件绝对路径
```
[root@fox01 shcode]# dirname /home/aaa/test.txt
/home/aaa
```

## 自定义函数
[ function ] funname[()]

{

	Action;

	[return int;]

}

调用直接写函数名：funname[值]
```
#!/bin/bash
# 计算输入2个参数的和动态的获取，getSum

function getSum() {
        SUM=$[ $n1+$n2]
        echo "$SUM"
}

read -p "n1=" n1
read -p "n2=" n2

getSum $n1 $n2
```

## 综合案例
```
#!/bin/bash
# 备份目录
BACKUP=/data/backup/db

# 当前时间
DATETIME=$(date +%Y-%m-%d_%H%M%S)
echo "start backup at $DATETIME..."

# 数据库地址
HOST=localhost

# 数据库用户名
DB_USER=root

# 数据库密码
DB_PW=

# 备份的数据库名称
DATABASE=lzsb

# 创建备份目录，如果不存在则创建
[ ! -d "${BACKUP}/${DATETIME}" ] && mkdir -p "${BACKUP}/${DATETIME}"
echo "backup path: ${BACKUP}/${DATETIME}/..."

# 备份数据库
mysqldump -u${DB_USER} -p${DB_PW} --host=${HOST} -q -R --databases ${DATABASE} | gzip > ${BACKUP}/${DATETIME}/$DATETIME.sql.gz

# 将文件处理成tar.gz
cd ${BACKUP}
tar -zcvf $DATETIME.tar.gz ${DATETIME}

# 删除对应的备份目录
rm -rf ${BACKUP}/${DATETIME}

# 删除10天前的备份文件
find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm -rf {} \;

echo "${DATABASE} backup done..."
```
```
[root@fox01 sbin]# crontab -l
#备份mysql  lzsb数据库
30 2 * * * /usr/sbin/mysql_db_backup.sh
```







































