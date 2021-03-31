---
title: mysql
date: 2021-01-08 15:44:47
tags:
---

### 假如 Mysql 忘记了密码
vim /etc/my.cnf   在【mysqld】的段中，加上skip-grant-tables
查看user表，修改即可，参考其他数据库user

设置查询缓存大小
SET GLOBAL innodb_buffer_pool_size=33554432;

## mysql 锁

- 乐观锁 （加版本）
- 悲观锁 （锁数据，行锁，事务） select xx for update


## mysql 事务4特性 ACID

数据库管理系统中事务(transaction)的四个特性（分析时根据首字母缩写依次解释）：
 - 原子性（Atomicity）、
 - 一致性（Consistency）、
 - 隔离性（Isolation）、
 - 持久性（Durability）

所谓事务，它是一个操作序列，这些操作要么都执行，要么都不执行，它是一个不可分割的工作单位。（执行单个逻辑功能的一组指令或操作称为事务）

## Mysql 三种日志

###  redo log （重做日志）

-  先写 内存 ，提交后再写入到磁盘中
-  存储在引擎innodb 
-  InnoDB引擎会把更新记录先写在redo log中，
-  在修改Buffer Pool中的数据， 当提交事务时，调用fsync把redo log刷入磁盘

###  undo log （回滚日志）
- 实现事务的原子性，也是存储在磁盘中
- 记录的是数据修改前的状态，在数据修改的流程中，同时会记录一条与当前操作相反的逻辑日志到undo log中。
- 如果遇到事务回滚，就借助 undo log 回滚到以前的状态
- undo log只负责记录事务开始前要修改数据的原始版本，当我们再次对这行数据进行修改，所产生的修改记录会写入到redo log，undo log负责完成回滚，redo log负责完成前滚

### bin log （归档日志）

- Server层 ，二进制形式存储在磁盘中
- 记录了数据库所有DDL和DML操作

### mysql 执行计划

