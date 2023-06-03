# 监控网络状态
netstat [opt]

-an    按一定顺序排列输出

-p     显示某个进程在调用

netstat -anp | more
```
[root@fox01 ~]# netstat -anp | grep sshd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      49884/sshd: /usr/sb 
tcp        0      0 192.168.200.131:22      192.168.200.1:55502     ESTABLISHED 53947/sshd: tom [pr 
tcp6       0      0 :::22                   :::*                    LISTEN      49884/sshd: /usr/sb 
unix  2      [ ]         STREAM     CONNECTED     105641   53947/sshd: tom [pr  
unix  3      [ ]         STREAM     CONNECTED     86753    49884/sshd: /usr/sb  
unix  3      [ ]         STREAM     CONNECTED     106615   53947/sshd: tom [pr  
unix  3      [ ]         STREAM     CONNECTED     106614   53968/sshd: tom@pts  
unix  2      [ ]         DGRAM      CONNECTED     106609   53947/sshd: tom [pr
```


