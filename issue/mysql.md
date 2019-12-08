# MySQL

### Ubuntu 安装后修改密码

> 系统：Ubuntu 18.04 版本：MySQL 5.7

安装后查看临时密码

```
# grep 'temporary password' /var/log/mysqld.log
```

提示文件不存在

```
grep: /var/log/mysqld.log: No such file or directory
```

那就换种方式改密码，检查 `mysqld` 状态

```
# service mysqld status
```

接着提示`mysqld`为无法识别的服务

```
mysqld: unrecognized service
```

然后把 `mysqld` 改成 `mysql` 就可以了

```
# service mysql status
 * MySQL is stopped.
# service mysql start
```

启动后使用 `mysqladmin` 修改密码

```
# mysqladmin -uroot password '123456'
```

尝试登陆

```
# mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 5.7.22-0ubuntu18.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

完成

#### 参考

<https://blog.csdn.net/heatdeath/article/details/78907563>

<http://blog.51cto.com/sf1314/2059215>
