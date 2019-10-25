---
title: ubuntu搭建lamp开发环境
date: 2018-03-09 15:12:00
tags: 工具
---

1.安装apache2  :
```bash
sudo  apt-get install  apache2
```
2.安装php5.6或其他版本：
使用ppa增加源:
```bash
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.0 php7.0-mysql php7.0-curl php7.0-json php7.0-cgi
```
或
关于php5.4–php5.6版本
```bash
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get -y install php5.6 php5.6-mcrypt php5.6-mbstring php5.6-curl php5.6-cli php5.6-mysql php5.6-gd php5.6-intl php5.6-xsl php5.6-zip
```
安装完成后，输入 php -v 查看当前的版本
3.安装mysql
```bash
sudo apt-get mysql-server
```

  至此，lamp 环境已经搭建完成。

  接下来就是修改apache2目录:
 *   cd /etc/apache2/sites-enabled
 *   vi 000-default.conf 默认的最好不用去修改 先到本地添加几个站点。
 *   vi /etc/hosts 增加就好了。不懂就直接百度了。

4.我们可以先配置多个站点，方便开发


 * cd /etc/apache2/sites-available
 * 看到有个000-default.conf 文件，
 * 直接cp 几份到当前目录就好了，逐渐设置根目录和域名。
 * 然后把这些文件cp 到 /etc/apache2/sites-enabled 这个目录下。
 * 记住需要到 cd /etc/apache2 vi apache2.conf
 * 把里面的None全部修改成All
 * 重启apache2 :service apache2 restart


5.到了这里，就配置成功了。欢迎分享。
