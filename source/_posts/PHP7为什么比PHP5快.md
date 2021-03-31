---
title: PHP执行原理和为什么PHP7比PHP5快
date: 2021-03-06 16:10:22
tags:
---

## php-fpm

- FastCGI
    - 一种协议，FastCGI是一个可伸缩地、高速地在HTTP server和动态脚本语言间通信的接口
    - 监听 事先启动，等待server 请求发起连接，并使用php-cgi 解析程序并返回结果
    - 一 master 多 worker 模式
    - 平滑启动
    
    
- php-fpm进程管理器
    php-fpm是对fastcgi协议的实现
    php-fpm是进程管理器，启动时包括master和worker进程俩部分，
    master进程负责管理worker进程，worker进程一般具有多个，用来监听端口，接收来自webserver请求，且每个worker进程都有一个cgi进程解释器，用来执行php代码




## 执行步骤

1. php初始化执行，启动zend引擎，加载已注册的扩展模块
2. 读取脚本文件，zend引擎对脚本进行词法分析、语法分析、生成语法生成树
3. zend引擎编译语法树，生成opcode中间代码
4. zend引擎执行opcode，返回执行结果

总结:
一段PHP代码会经过词法解析、语法解析等阶段，会被翻译成一个个指令（opcode），然后 zend 虚拟机会顺序执行这些指令。


### 概念

zval： 变量内存存储结构

hashTable： 数据结构

HashTable 结构中有bucket ，bucket 有zval[0],zval[1]





## PHP7主要优化点

- 变量存储优化

- 数组存储优化
zend_string 存放了key，hash，元素和hash映射表内存共享

- hashtable存储优化
存储连续的内存中，不在通过指针指向




####  ZVAL 结构体（保存内存变量的结构）
hashtable 

1. PHP5 

- _zval_struct总的字节 = value（16）+ refcount__gc（4）+ type（1）+ is_ref__gc（1） + 内存对齐2 = 占用22字节。
- HashTable 占用72字节
- burst IO  2次，64为一次
- bucket  72 字节 存放zval

2. PHP7

- zval_struct 占用16字节
- HashTable/ zend_array  占用 57字节 （向内存索取空间，默认每次是64字节，不够再向内存索取）
- burst IO  一次
- bucket  32 字节




PHP 5 到 PHP 7.0 HashTable 主要做了如下修改

优化 HashTable 的数据结构：
一个 PHP 数组 zend_array 的内存占用从PHP5点72个字节，降低到了56个字节
使用内存缓存局部性的特点，优化 PHP 数组效率
PHP 5 的 Bucket ，包括 zval 都是独立分配（在内存中是离散的）
PHP 7 中使用一块连续的空间存储  Bucket，并且一个 Bucket 中包含一个 zval 数据，即 Bucket 和 zval 在内存中都是连续存储的