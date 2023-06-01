# at 定时任务
## 一次性定时计划任务
## 保证atd进程的启动

ps -ef i           检测当前运行进程
ps -ef | grep atd  检测atd是否在运行

at [opt] [time]
-m
-I
-d
-v
-c
-V
-q <队列>
-f <文件>
-t <时间参数>


## 输入结束后按  2次 ctrl+D
01: 两天后下午五点
    atq 查看有没有执行的工作任务
```
[root@192 home]# at 5pm + 2 days
warning: commands will be executed using /bin/sh
at> /bin/ls /home<EOT>
job 1 at Sat Jun  3 17:00:00 2023
[root@192 home]# atq
1	Sat Jun  3 17:00:00 2023 a root
```

02: 明天17点，输出时间到指定文件
```
[root@192 home]# at 5pm tomorrow 
warning: commands will be executed using /bin/sh
at> date > /root/date100.log<EOT>
job 2 at Fri Jun  2 17:00:00 2023
[root@192 home]# atq
2	Fri Jun  2 17:00:00 2023 a root
1	Sat Jun  3 17:00:00 2023 a root
```

03: 2分钟后写入文件
```
[root@192 home]# at now + 2 minutes
warning: commands will be executed using /bin/sh
at> date > /root/date200.log<EOT>
job 3 at Thu Jun  1 20:39:00 2023
[root@192 home]# atq
2	Fri Jun  2 17:00:00 2023 a root
3	Thu Jun  1 20:39:00 2023 a root
1	Sat Jun  3 17:00:00 2023 a root
```

04: 删除已经设置的任务，atrm编号
```
[root@192 home]# atrm 1
[root@192 home]# atq
2	Fri Jun  2 17:00:00 2023 a root
```









