---
title: Redis-持久化
date: 2021-01-12 14:48:25
tags:
---


### RDB （redis database）
    
- 二进制文件dump.rdb
-  save方式 save 300 10  （300s 内有10次改动 就save ）
-  bgsave 



### AOF （append only file）

- 文件追加
- appendonly yes
- AOF可以解决数据持久化的实时性问题



启动优先级：
假设Redis 同时打开了RDB和AOF持久化功能，当Redis重启的时候会优先加载AOF，因为AOF数据更新的频率更高，会保存更新的数据。
  
rdb 更快，实时性。
