---
layout: docker搭建php7 + nginx
title: docker搭建php7 + nginx
date: 2018-04-28 17:31:28
tags: [docker,nginx]
---
1. 安装docker

2. 下载相关镜像
```bash
  docker pull nginx
  docker pull php:7.1.0-fpm
```
3. 建立相关挂载目录
```bash
  mkdir -p /docker/www
  mkdir -p /docker/nginx/conf.d
```
4. nginx 配置
```bash
    vim /docker/nginx/conf.d/default.conf
    ## 例子
    server {
    listen  80 default_server;
    server_name _;
    root   /usr/share/nginx/html;

    location / {
      index index.html index.htm index.php;
      autoindex off;
    }
    location ~ \.php(.*)$ {
      root   /var/www/html/;
      fastcgi_pass myphp:9000;
      fastcgi_index index.php;
      fastcgi_split_path_info ^((?U).+\.php)(/?.+)$;
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      fastcgi_param PATH_INFO $fastcgi_path_info;
      fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
      include  fastcgi_params;
     }
    }
```
5. 启动php镜像,nginx 镜像

  1. php 端口映射启动
```bash
  docker run -p 9000:9000 --name myphp \
  -v /docker/www/:/var/www/html/ \
  --privileged=true \
  -d php:7.1.0-fpm
```
  2. nginx 端口映射启动
```bash
docker run -p 80:80 --name mynginx \
-v /docker/www:/usr/share/nginx/html \
-v /docker/nginx/conf.d:/etc/nginx/conf.d \
--privileged=true \
-d nginx
```
6. 自行配置需要的项目和站点conf
```bash
  查看运行的容器 ： docker ps -a
  停止，启动，重启   docker stop start restart  id
  删除容器： docker  rm  id
```
  todo 多站点再完善！！！

7. 重启nginx镜像
```bash
docker restart mynginx
```


参考地址： http://www.jb51.net/article/113296.htm
