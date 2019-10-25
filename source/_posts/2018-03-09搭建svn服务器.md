---
layout: centos
title: 搭建svn服务器
date: 2018-03-08 16:51:00
tags: 工具
---
## 步骤
1. 安装svn  :   
```bash
 yum install subversion
 ```
2. 切换到home目录并创建svn文件：
bash
cd /home  mkdir svn

 * 创建项目目录：cd svn mkdir project
 * 使用svn 创建svn配置文件 ： svnadmin create /home/svn/project
 * 修改配置文件：
cd /data/svn/project/conf/
进入conf目录，然后编辑svnserve.conf、authz和passwd文件。
具体的，可以参考以下内容进行编辑。

    * 编辑 svnserve.conf文件
```bash
[root@arui conf]# vi svnserve.conf
[general]
anon-access = none
auth-access = write
password-db = passwd
authz-db = authz
realm = project
```
    * 编辑authz文件
```bash
[root@arui conf]# vi authz
[groups]
manager=test
[project:/]
@manager = rw
```
    * 给project仓库添加一个名称为test的用户，权限为读写。

    * 编辑passwd文件
```bash
[root@arui conf]# vi passwd
test = 123456
```
       将test用户的密码设置为123456

## 启动svn 服务

```bash
  svnserve -d -r /home/svn/project
```

## 开启防火墙

  * 使用SVN客户端连接到svn://VPS IP/project，根据提示输入用户名test、密码123456，如果顺利，即可连接成功。
  * 如果无法连接，可能是VSP服务器的3690端口未开放，此时可以用telnet测试下。如果未开放，需要在VPS上设置Iptable解除端口限制。
```bash
vi /etc/sysconfig/iptables
添加：
-A OUTPUT -p tcp -m tcp –dport 3690 -jACCEPT
```
  * 以后即可在其他地方访问svn了.


使用示例：
```bash
svn import /data/test svn://ip/svn/project/myapp/ -m ‘f’ –force;
```
按照提示输入用户名和密码，然后就创建一个库成功了。
关于一点错误提示：
svn: E170001报错的原因以及解决方案
默认情况下是记录了开始输入的账户密码，需要清除才能验证：
```bash
rm -rf /root/.subversion/auth/
```
