---
title: guzzle异步发送
date: 2018-04-23 17:05:14
tags:
---
## 第一步
```bash
composer require guzzlehttp/guzzle 6.3.3
```
## 发起同步请求(参考)
```bash
$client = new \GuzzleHttp\Client();
$res = $client->request('GET', 'https://api.github.com/repos/guzzle/guzzle');
echo $res->getStatusCode();
echo $res->getHeaderLine('content-type');
echo $res->getBody();

```

## 发起异步请求
```bash
//Send an asynchronous request.
    $request = new \GuzzleHttp\Psr7\Request('GET', 'http://httpbin.org');
    $promise = $client->sendAsync($request)->then(function ($response) {
                echo 'I completed! ' ;
                //$response->getBody();
            });
               echo "5";
               echo "zs";
        $promise->wait();
```

```bash
  输出结果：5 zsI completed!

```
 ######  这里promise wait 什么时候调用，就什么时候出echo 的结果
