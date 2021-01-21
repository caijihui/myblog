---
title: mysql-log
date: 2021-01-08 15:44:47
tags:
---


## mysql 锁

- 乐观锁 （加版本）
- 悲观锁 （锁数据，行锁，事务） select xx for update



## Mysql 三种日志

###  redo log （重做日志）

-  存储在引擎innodb 
-  InnoDB引擎会把更新记录先写在redo log中，
-  在修改Buffer Pool中的数据， 当提交事务时，调用fsync把redo log刷入磁盘

###  undo log （回滚日志）

- 记录的是数据修改前的状态，在数据修改的流程中，同时会记录一条与当前操作相反的逻辑日志到undo log中。
- 如果遇到事务回滚，就借助 undo log 回滚到以前的状态
- undo log只负责记录事务开始前要修改数据的原始版本，当我们再次对这行数据进行修改，所产生的修改记录会写入到redo log，undo log负责完成回滚，redo log负责完成前滚

### bin log （归档日志）

- Server层 ，二进制形式存储在磁盘中
- 记录了数据库所有DDL和DML操作
