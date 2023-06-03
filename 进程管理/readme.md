# 进程管理

## 1. Linux中每一个执行的程序都成为一个进程，每一个进程都分配一个ID pid，进程号。

## 2. 每个进程都以2中方式存在。前台与后台。

## 3. 一般系统的服务都是以后台进程的方式存在，并且会常驻在系统中。直到关机方才结束。

ps -a:
ps -u:
ps -x:
ps -aux | more

```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.8 173312 15288 ?        Ss   20:39   0:01 /usr/lib/systemd/systemd rhgb --switched-root --system --deserialize 31
root           2  0.0  0.0      0     0 ?        S    20:39   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   20:39   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   20:39   0:00 [rcu_par_gp]
root           5  0.0  0.0      0     0 ?        I<   20:39   0:00 [slub_flushwq]
root           6  0.0  0.0      0     0 ?        I<   20:39   0:00 [netns]
```

![process](./process.png)

查看进程
ppid: 父进程
```
[root@fox01 ~]# ps -ef | grep sshd
root         851       1  0 20:39 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 1 of 10-100 startups
root        6755     851  0 21:26 ?        00:00:00 sshd: root [priv]
sshd        6756    6755  0 21:26 ?        00:00:00 sshd: root [net]
root        6758     851  0 21:26 ?        00:00:00 sshd: tom [priv]
tom         6780    6758  0 21:26 ?        00:00:00 sshd: tom@pts/1
root        6858    6821  0 21:27 pts/1    00:00:00 grep --color=auto sshd

```

# 终止进程kill和killall
## kill [opt] pid
## kill 进程名称
-9 强迫进程立即停止

·kill sshd然后重启服务
```
[root@fox01 ~]# ps -ef | grep sshd
root         851       1  0 20:39 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root        7464    4167  0 21:44 pts/0    00:00:00 grep --color=auto sshd
[root@fox01 ~]# kill 851
[root@fox01 ~]# /bin/systemctl start sshd.service 
[root@fox01 ~]# 
[root@fox01 ~]# ps -ef | grep sshd
root        7529       1  0 21:47 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root        7539    4167  0 21:47 pts/0    00:00:00 grep --color=auto sshd
```

·终止多个任务
killall geidt

·强制杀掉一个终端
```
[root@fox01 桌面]# ps -aux | grep bash
root        4167  0.0  0.3 224652  5840 pts/0    Ss+  20:39   0:00 bash
root        8285  0.1  0.3 224272  5764 pts/1    Ss   21:55   0:00 bash
root        8320  0.0  0.1 221388  1884 pts/1    S+   21:55   0:00 grep --color=auto bash
[root@fox01 桌面]# kill 4167
[root@fox01 桌面]# kill -9 4167
```

# pstree
```
[root@fox01 桌面]# pstree -u
systemd─┬─ModemManager───3*[{ModemManager}]
        ├─NetworkManager───2*[{NetworkManager}]
        ├─VGAuthService
        ├─accounts-daemon───3*[{accounts-daemon}]
        ├─atd


[root@fox01 桌面]# pstree -p
systemd(1)─┬─ModemManager(769)─┬─{ModemManager}(774)
           │                   ├─{ModemManager}(776)
           │                   └─{ModemManager}(780)
           ├─NetworkManager(792)─┬─{NetworkManager}(795)
           │                     └─{NetworkManager}(796)
           ├─VGAuthService(718)
           ├─accounts-daemon(712)─┬─{accounts-daemon}(724)
           │                      ├─{accounts-daemon}(725)
           │                      └─{accounts-daemon}(727)
           ├─atd(1107)

```

































