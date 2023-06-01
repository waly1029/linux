# Group

示例:
```
[root@192 home]# ls -lah  
总用量 5.8M  
drwxr-xr-x.  6 root root 4.0K  6月  1 15:47 .  
dr-xr-xr-x. 19 root root 4.0K  6月  1 11:48 ..  
drwxr-xr-x.  2 root root 4.0K  6月  1 15:36 bbb  
-rw-r--r--.  1 root root   60  6月  1 15:31 hello.txt  
-rw-r--r--.  1 root root  607  6月  1 14:58 info.txt  
drwx------.  4 jack jack 4.0K  5月 31 23:37 jack  
-rw-r--r--.  1 root root 3.8M  6月  1 15:46 myhome.tar.gz  
-rw-r--r--.  1 root root 2.0M  6月  1 15:39 myhome.zip  
-rw-r--r--.  1 root root  479  6月  1 15:44 pc.tar.gz  
drwx------. 14 tom  tom  4.0K  6月  1 15:16 tom  
drwx------.  3 zwj  gb   4.0K  5月 31 23:45 zwj  
```

改变文件或者目录所有者
```
chown tom apple
```

创建组 用户
groupadd artists
useradd -g artists fox
```
[root@192 home]# groupadd artists
[root@192 home]# useradd -g artists fox
[root@192 home]# id fox
用户id=1005(fox) 组id=1006(artists) 组=1006(artists)
```

```
[fox@192 ~]$ touch apple2
-rw-r--r--. 1 fox  artists    0  6月  1 16:18 apple2
```

修改文件所在组
```
[root@192 ~]# chgrp fruit orange

```

改变用户所在组
usermod -g 新组名 用户名
usermod -d 目录名 用户名 改变该用户登录的初始目录。### 用户需要有进入到新目录的权限 ###
