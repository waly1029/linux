# 磁盘情况查询

```
[root@192 桌面]# df -h
文件系统        容量  已用  可用 已用% 挂载点
devtmpfs        4.0M     0  4.0M    0% /dev
tmpfs           854M     0  854M    0% /dev/shm
tmpfs           342M  6.8M  335M    2% /run
/dev/nvme0n1p3   16G  6.0G  9.2G   40% /
/dev/nvme0n2p4  989M   24K  922M    1% /newdisk
/dev/nvme0n1p2  974M  218M  689M   25% /boot
/dev/nvme0n1p1  599M  7.0M  592M    2% /boot/efi
tmpfs           171M   92K  171M    1% /run/user/0
/dev/sr0        7.6G  7.6G     0  100% /run/media/root/CentOS-Stream-9-BaseOS-aarch64
```
80%就需要处理

du命令使用
```
[root@192 opt]# du -h --max-depth=1 /opt
4.0K	/opt/bbb
12M	/opt/tmp2
9.3M	/opt/tmp
172M	/opt/rh
192M	/opt

[root@192 opt]# du -ha --max-depth=1 /opt
4.0K	/opt/bbb
0	/opt/cat
12M	/opt/tmp2
9.3M	/opt/tmp
172M	/opt/rh
192M	/opt

[root@192 opt]# du -hac --max-depth=1 /opt
4.0K	/opt/bbb
0	/opt/cat
12M	/opt/tmp2
9.3M	/opt/tmp
172M	/opt/rh
192M	/opt
192M	总用量
```

# 磁盘实用指令
正则表达式 "^-"，以-开头的所有文件也就是非dir文件
wc -l 统计文件数量
```
[root@192 opt]# ls -l | grep "^-"
-rw-r--r--. 1 root root    0  6月  1 21:59 cat
-rw-r--r--. 1 root root    0  6月  2 11:19 knight.md
-rw-r--r--. 1 root root    0  6月  2 11:19 pig.md

[root@192 opt]# ls -l | grep "^-" | wc -l
3

[root@192 opt]# ls -l | grep "^d" | wc -l
4
```

并统计子文件夹中文件
```
[root@192 opt]# ls -lR | grep "^-" | wc -l
1192
```

树状显示目录结构
```
[root@192 opt]# tree /home
/home
├── abc
├── app
├── apple
├── bajie
├── bbb
│   ├── cat.txt
│   ├── dog.txt
│   ├── fuck.txt
│   └── pig.txt
├── fox
│   ├── apple
│   └── apple2
```




































