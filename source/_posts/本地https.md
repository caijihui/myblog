---
title: 本地https
date: 2018-06-08 11:49:56
tags: https
---
## 生成证书
1. 使用openssl生成密钥privkey.pem：
```bash
 sudo openssl genrsa -out privkey.pem 1024/2038
```

2. 使用密钥生成证书server.pem：
```bash
openssl req -new -x509 -key privkey.pem -out server.pem -days 365
```
证书信息可以随便填或者留空，只有Common Name要根据你的域名填写。

以我的本地网站为例
Common Name (e.g. server FQDN or YOUR name) []: test.com

也可以通过*.test.com来匹配你的二级域名

## 配置nginx
```bash
server {
    listen 80
    listen 443 ssl;
    server_name test.com;

    ssl on;
    ssl_certificate /path/to/server.pem;
    ssl_certificate_key /path/to/privkey.pem;
  ...
}
```
重启服务器
## 配置本地信任站点

浏览器打开 https://test.com

这时显示不安全图标。打开开发者模式，Security，View certificate，把看到的test.com 证书拖到本地的桌面，到系统里面去设置证书状态为信任即可。


参考地址：https://segmentfault.com/a/1190000007990972
