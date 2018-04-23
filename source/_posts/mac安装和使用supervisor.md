---
title: mac安装和使用supervisor
date: 2018-03-09 15:02:05
tags: 工具
---
##

1.安装和启动supervisor

```bash
    brew install supervisor
    brew services start supervisor
  ```

2.修改配置文件

```bash
    vi /usr/local/etc/supervisord.ini
    ##找到如下部分： 把前面的注释去掉
    [inet_http_server]         ; inet (TCP) server disabled by default
    port=127.0.0.1:9001        ; ip_address:port specifier, *:port for all iface
    username=user              ; default is no username (open server)
    password=123               ; default is no password (open server)
```

3.创建进程任务

```创建目录和文件
mkdir supervisor.d      
vi  queue_mm.ini
```
  文件内容格式如下 ：
```
[program:queue_mm]    //进程名称
process_name=%(program_name)s_%(process_num)02d
command=php /Users/facevisa/caijihui/laravel/artisan queue:work  beanstalkd –queue=mm   // 命令
autostart=true      //设置开启
autorestart=true   //设置重启
numprocs=1         //进程启动数
redirect_stderr=true
stdout_logfile=/Users/facevisa/my/laravel//storage/logs/queue_mm.log //日志文件
```

4.重启服务
```bash   
  brew services restart supervisor
```

5.测试   
```
在命令行输入   supervisorctl    
如果出现  http://localhost:9001 refused connection   
参考第三步，取消注释；如无提示，就ok
```

7、至此，就安装成功了
