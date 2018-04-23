---
title: php异步调用
date: 2018-03-16 13:18:35
tags: php
---

## php异步调用方法  
 ##### 介绍我经常用的而且官方也推荐的
 * 直接上代码：
```bash
    public function doRequest($host,$path, $param=array()){  
        $query = isset($param)? http_build_query($param) : '';   

        $port = 80;   
        $errno = 0;   
        $errstr = '';   
        $timeout = 10;   

        $fp = fsockopen($host, $port, $errno, $errstr, $timeout);   

        $out = "POST ".$path." HTTP/1.1\r\n";   
        $out .= "host:".$host."\r\n";   
        $out .= "content-length:".strlen($query)."\r\n";   
        $out .= "content-type:application/x-www-form-urlencoded\r\n";   
        $out .= "connection:close\r\n\r\n";   
        $out .= $query;   

        fputs($fp, $out);  
        fclose($fp);   
    }  
```

##  以 post 请求为例，异步调用
```bash
 * 参数说明：参数1[请求目标地址的主域名]，参数2[路劲，一般是"入口文件/模块/控制器/操作方法"，当然也不排除你的单个php文件访问，后面就是你要进行传递的数据了了]  
public function yibutest(){  
    $this->doRequest('a.tests.com','/api.php/User/Users/login',array(  
        'username'=>'test001',  
        'pwd'=>'123456'
        )  
    );  
    return array("code":1);
}
```

 * 参考地址：
 http://blog.csdn.net/df981011512/article/details/73866340
