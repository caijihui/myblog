---
title: 本地配置的 *.dev,*.app域名 在谷歌浏览器中总是自动转跳到https 导致不能访问
date: 2018-03-09 13:21:33
tags: 常见问题
---

由于 Chrome 升级了浏览器版本到 63，现在所有的 .dev 和 .app 都将会自动将 HTTP 到 HTTPS 上，
原因是谷歌已经拿下了 .dev 的顶级域名；
目前唯一的方法就是修改你的 .dev 或者 .app 域名了，或者换成火狐或者其他浏览器开发；
建议将你的域名改成 .test 或者 .localhost



## 参考地址：https://segmentfault.com/q/1010000012339191
