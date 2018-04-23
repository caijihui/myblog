---
title: redis基础操作
date: 2018-03-09 13:48:48
tags: redis
---

1、redis key-value
```bash
$redis->set($key,$value);
$redis->get($key);
$redis->exists($key);
```
2、redis订阅发布： —未实现，阻塞
```bash
   $redis=new Redis();
   $redis->connect(“127.0.0.1”,6379);
   $redis->auth(“123”);
   $redis->publish(‘test.22’,”nihao”);
   $redis->publish(‘test’,”nihao”);
   $channelName=”test”;
   $redis->subscribe(array($channelName), ‘callback’);
   function callback($redis,$channelName,$message){
     echo $message;
   }
 ```
3、redis 先进先出，队列
```bash
 $redis->lpush(“test”, “3”);
 $redis->lpush(“test”, “2”);
 $redis->Rpop(‘test’);
 $arrList = $redis->lrange(“test”, 0 ,2);
 print_r($arrList);
 ```

4、排行操作

```bash
  //增加积分,会员名，分数
    public function addScores($memeber, $scores){
        $redis=new Redis();
        $redis->connect(“127.0.0.1”,6379);
        $redis->auth(“123”);
        $key = date(‘Ymd’);
        return $redis->zIncrBy($key, $scores, $memeber);
    }
    //获取排名,$date 作为key
    public function getRank($date, $start, $stop){
        $redis=new Redis();
        $redis->connect(“127.0.0.1”,6379);
        $redis->auth(“123”);
        $key=$date;
        return $redis->zRevRange($key, $start, $stop, true);
    }
    实例：
            //增加积分
            $this->addScores(‘zs’,5);
            $this->addScores(‘ls’,8);
            $this->addScores(‘ww’,2);
            $this->addScores(‘wl’,2);
            $this->addScores(‘lw’,10);
            //获取排名
           $this->getRank($key,0,2);
```

5、redis判断登录和注册：

```bash
      $mobile=$_POST[‘mobile’];
      $hmobile=”user:{$mobile}”;//此处是设置key
      $r= $redis->exists($hmobile);//是否存在
      $m=$redis->hExists($hmobile,”mobile”);//也可以判断存在 返回为bool
      if ($r==0){
      $mobile=$_POST[‘mobile’];
      $name=$_POST[‘mobile’];
      $pwd=$_POST[‘pwd’];
      $age=$_POST[‘age’];
      //   HSET  key field value   哈希的格式
      $redis->hSet($hmobile,”name”,$name);
      $redis->hSet($hmobile,”mobile”,$mobile);
      $redis->hSet($hmobile,”pwd”,$pwd);
      $redis->hSet($hmobile,”age”,$age);
      echo “注册成功！”;
    }else{
        echo “存在，不可注册”;
    }
    $all= $redis->hGetAll($key); //当前key的所有字段 结果 ，返回的是数组
        dump($all);
        $s=$redis->hGet($key,”mobile”);//单个字段的结果
        dump($s);
```
