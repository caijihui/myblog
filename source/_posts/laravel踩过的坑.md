---
title: laravel踩过的坑
date: 2019-01-14 15:27:19
tags:
---

## ORM  get() 查询无数据,为空处理
可以通过以下方式验证数据是否为空
```php
 $users = DB::table('users')->where('pid',1)->get();
  if ($users->first()) {
      //
   } 
  if (!$users->isEmpty()) {
      //
   } 
  if ($users->count()) {
      //
   }
 
```
## ORM first() 为空处理

```php
   $userInfo = DB::table('users')->where('pid',1)->orderBy('id','desc')->first(); 
   if($userInfo){
        //
   }
   if($userInfo !== null){
        //
   }
   
```


## /routes/web.php  POST 请求 报419

```p
419 unknown status
一般是发送的请求有 csrf-token校验,但是你没有发送csrf-token这个参数，注意查看http头是否带有csrf-token
可以在 /app/Http/Kernel.php 
把 \App\Http\Middleware\VerifyCsrfToken::class, 注释掉，以后post 请求就不用填加csrf-token 参数头了
```

## null false  比较语法
```php
$res = false;
if(null !== $res){
    echo "11";
}else{
    echo "22";
}
11

if(null != $res){
    echo "r0";
}else{
    echo "r1";
}

r1

```
空字符串('')，false,NULL和0是值相等而类型不一样,不能使用=== !== 进行比较 。

