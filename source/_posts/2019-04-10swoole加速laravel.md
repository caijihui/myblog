---
title: swoole加速laravel
date: 2019-04-10 16:44:41
tags: [swoole,laravel]
---
（以laravel 为例）
现有轮子：

- swooletw/laravel-swoole
-  garveen/laravoole


1. 安装
    ```bash
        composer require swooletw/laravel-swoole
    ```

2. 在 config/app.php 的 providers 数组中加上
    ```bash
        SwooleTW\Http\LaravelServiceProvider::class,
    
    ```
3. 配置文件执行命令或在config文件夹创建swoole_http.php
    ```bash
        php artisan vendor:publish --provider="SwooleTW\Http\HttpServiceProvider"
    
    ```
    去 config/swoole_http.php 中配置信息
    ```php
       'server' => [
               'host' => env('SWOOLE_HTTP_HOST', '0.0.0.0'),//监听任意ip
               'port' => env('SWOOLE_HTTP_PORT', '1215'),
               'options' => [
                   'pid_file' => env('SWOOLE_HTTP_PID_FILE', base_path('storage/logs/swoole_http.pid')),
                   'log_file' => env('SWOOLE_HTTP_LOG_FILE', base_path('storage/logs/swoole_http.log')),
                   'daemonize' => env('SWOOLE_HTTP_DAEMONIZE', 1),//1-程序将转入后台作为守护进程运行
               ],
       ],
    ```
4. 启动swoole HTTP服务

    ```php
        ## 启动
        php artisan swoole:http start
            
        ## 重启    
        php artisan swoole:http restart
    ```
    打开 [http://127.0.0.1:1215](http://127.0.0.1:1215)，即可访问应用
    
    `不支持热启动`，每次需要重启。
    
5. nginx 配置,支持热启动
 
```nginx
    server {
        listen 80;
        server_name stu.com;
        root /path/app/ublic;
        index index.php;
    
        location = /index.php {
            # Ensure that there is no such file named "not_exists"
            # in your "public" directory.
            try_files /not_exists @swoole;
        }
    
        location / {
            try_files $uri $uri/ @swoole;
        }
    
        location @swoole {
            set $suffix "";
    
            if ($uri = /index.php) {
                set $suffix "/";
            }
    
            proxy_set_header Host $host;
            proxy_set_header SERVER_PORT $server_port;
            proxy_set_header REMOTE_ADDR $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    
            # IF https
            # proxy_set_header HTTPS "on";
    
            proxy_pass http://127.0.0.1:1215$suffix;
        }
    }

```
    

参考：[https://segmentfault.com/a/1190000017553188](https://segmentfault.com/a/1190000017553188)