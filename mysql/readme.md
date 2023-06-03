# mysql
## yum 安装mysql
启动服务: systemcl start mysqld.service

如果有默认密码查看:

grep "password" /var/log/mysqld.log

如果没有密码直接enter进入即可
```
[root@fox01 mysql]# mysql -u root -p
Enter password:
```

重新设置密码:
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
Query OK, 0 rows affected (0.01 sec)
```

