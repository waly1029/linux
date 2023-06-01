# linux 权限

```
drwxr-xr-x. 2 root root  4096  5月 31 19:34 桌面
-rw-------. 1 root root  1405  5月 31 18:39 anaconda-ks.cfg
```
### drwxr-xr-x ###
0: 文件类型(d,-,l,c,b)
   l 链接文件，快捷方式
   d 文件夹，目录
   - 普通文件
   c 字符文件
   b 块设备，比如硬盘
1-3: 文件所有者的权限
4-6: 所属组的权限
7-9: 其他组的权限

rwx作用到文件
r: 查看，读取
w: 可修改，不代表可删除，删除前提是### 对该文件所在文件夹有w权限 ###，才能删除
x: 可执行

## rwx作用到目录 ##
r: 可读取，ls查看
w: 可修改，创建+删除+重命名
x: 可进入

chmod u=rwx,g=rx,o=x 文件/目录名
chmod o+w file
chmod a-x file    a是all所有组
chmod 751 file

chown newowner file/dir 改变所有者
-R 递归
改变所有者
```
chown tom /home/abc.txt
```
改变目录下所有文件和目录改成tom
```
chown -R tom /home/dir
```

chgrp newgroup file/dir 改变所在组


