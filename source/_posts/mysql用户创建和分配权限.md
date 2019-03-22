---
title: mysql用户创建和分配权限
date: 2018-08-21 16:31:38
tags: mysql
---


### Mysql 创建用户和分配权限

> 1. 创建用户

```mysql
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

- username - 你将创建的用户名,
- host - 指定该用户在哪个主机上可以登陆，此处的"localhost"，是指该用户只能在本地登录，不能在另外一台机器上远程登录，如果想远程登录的话，将"localhost"改为"%"，表示在任何一台电脑上都可以登录;也可以指定某台机器可以远程登录;
- password - 该用户的登陆密码,密码可以为空,如果为空则该用户可以不需要密码登陆服务器。


	如果遇到 ERROR 1819 (HY000): Your password does not satisfy the current policy requirements  ,是由于mysql 密码安全策略，执行下方语句即可

```mysql
	set global validate_password_policy=0;
```

> 2. 分配权限

```mysql
GRANT (all,select,insert,update) privileges ON databasename.tablename TO 'username'@'host' identified by 'password';
```

- privileges 用户的操作权限,如SELECT , INSERT , UPDATE 等(详细列表见该文最后面).如果要授予所的权限则使用ALL.;
databasename - 数据库名,tablename-表名,如果要授予该用户对所有数据库和表的相应操作权限则可用*表示, 如 *.*.


```mysql
flush privileges;
```

###  example 
    
```mysql

    ## 查看所有用户
    select * from mysql.user；
    ##  创建拥有全部权限的用户
    GRANT all privileges ON *.* TO 'test'@'%' identified by 'pwd';
    ##  创建拥有查看权限的用户
    GRANT select privileges ON *.* TO 'test'@'%' identified by 'pwd';
    ##  创建只拥有查看 test 数据库 user 表数据的 权限的用户
    GRANT select privileges ON test.user TO 'test'@'%' identified by 'pwd';
    
    ## 执行刷新
    flush privileges;

```