# reset root passwd
1. reboot machine and press ESC to select enter mode
2. #mount -o remount,rw /
3. #passwd
4. #touch /.autorelabel
5. #exec /sbin/init

# man查看命令
#ls
-a 查看所以文件
#ls -a
-l 单行输出
#ls -l
-la 单行输出所以，选项可以组合输出
#ls -al /root
ls -lh 显示文件大小人性化

# help
## 获取shell内置命令帮助信息
#help cd

# pwd
## 当前工作目录绝对路径

# cd
cd~ 回到当前用户的家目录
cd.. 回到当前目录上一级

# mkdir
## 创建目录
-p: 创建多级目录

# rmdir
#rmdir /home/animal 删除空文件夹
递归删除
#rm -rf /home/animal/

# touch

# cp
## cp [选项] source dest
## -r 递归拷贝
#\cp -r /home/bbb /opt  强制覆盖

# rm
##删除文件或目录
-r 递归删除
-f 强制删除不提示

# mv
mv oldNameFile newNameFile  重命名
mv /temp/movefile /targetFolder  移动文件

# cat
只浏览不修改
cat [opt] file
-n 显示行号
#cat /etc/profile -n | more     |是管道命令，cat时more可以分页查看

# more
交互指令
Enter 一行
space 一页
ctrl+f 下滚动一页
ctrl+b 返回上一页
= 输出行号
:f 输出文件名和当前行号

# less
对于查看大型文件具有较高效率
space 下一页
pagedown 下一页
pageup 上一页
/子串 向下搜寻 n:向下查找; N:向上查找
?子串 向上搜寻 n:向下查找; N:向上查找


# echo
echo [opt] [content]
echo 指令输出环境变量: $PATH $HOSTNAME
echo 指令输出hello,world!
echo "hello" > data.txt  覆盖重定向
echo "hello" >> data.txt  追加重定向

# head
查看文件前10行
head file
head -n 5 file

# tail
文件尾部
tail -n 5 /etc/profile
tail -f file 实时追踪

# > 和 >>
ls -l > file       (列表中的内容写入file中，覆盖)
ls -al >> file     (列表中的内容追加到file的末尾)
cat file1 > file2  (文件1内容覆盖到文件2)

# cal
日历

# ln
类似快捷方式
ln -s [源文件或目录] [软链接名]

# history
history 10
!5  执行第五条历史命令


# 时间日期类指令
# date
date
date + %Y
date + %m
date + %d
date "+%Y-%m-%d %H:%M:%S"
date -s 字符串时间

# cal
cal
cal 2023

# 搜索查找类指令
# find
find [搜索范围][opt]
-name <查询方式>
-user <用户名>
-size <文件大小>
find /home -name hello
find /opt -user nobody
find / -size +200M

# locate
每次运行前，必须使用updatedb创建locate数据库

# which
查看指令在哪个目录
which ls

# grep
过滤查找和管道符|使用
grep [opt] 查找内容 源文件
-n 行号
-i 忽略大小写字母
cat hello.txt | grep -n "yes"
grep -n "yes" /home/hello.txt

# 压缩和解压
# gizp/gunzip
gzip file ===> *.gz
gunzip file.gz

# zip/unzip
zip -r
unzip -d <目录>
zip -r myhome.zip /home/ 将home及其子文件和文件夹压缩
unzip -d /opt/tmp /home/myhome.zip

# tar
-c 产生.tar打包文件
-v 详细信息
-f 指定压缩后的文件名
-z 打包同时压缩
-x 解包.tar文件
tar [opt] XXX.tar.gz
tar -zcvf pc.tar.gz cat.txt dog.txt info.txt
tar -zxcf myhome.tar.gz -C /opt/tmp2
























