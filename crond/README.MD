# Crond
## 任务调度：特定时间执行的任务等
## 如重复工作，mysql备份等

-e 编辑定时任务
-l 查询任务
-r 删除任务

service cron restart 重启调度任务

执行命令
```
crontab -e
```

每一分钟执行一次命令
第一个*    每小时中的第几分钟    0-59
第二个*    每天中的第几个小时    0-23
第三个*    每个月中第几天        1-31
第四个*    每年中第几个月        1-12
第五个*    每周中星期几          0-7     0和7都是星期天

*    每一小时每分钟都执行一次
,    不连续时间 "0 8,12,16 * * *", 每天8点0分，12点0分，16点0分都执行一次
-    连续时间 "0 5 * * 1-6", 周一至周六凌晨5点0分执行
*/n  每隔多久执行一次，"*/10 * * * *", 每隔10分钟执行一次命令
```
*/1 * * * * ls -l /etc/ > /tmp/to.txt
```

执行脚本,my.sh需要有执行权限 chmod u+x my.sh
```
*/1 * * * * /home/my.sh
```

备份数据库
```
0 2 * * * mysqldump -u root -p 密码 数据库 > /home/db.bak
```
