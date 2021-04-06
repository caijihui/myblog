---
title: 类 self和static区分
date: 2019-07-30 09:48:14
tags: Class
---

类的静态延迟绑定
在 PHP 类中，self指向的是当前方法存在的这个类，也就是父类。static指向的是最终那个子类。

### self
取决于定义当前方法所在的类,调用当前所在层的方法。


```php

    class A {
        public static function who() {
            echo __CLASS__;
        }
        public static function test() {
            self::who();
        }
    }
    
    class B extends A {
        public static function who() {
            echo __CLASS__;
        }
    }
    B::test();//A
```



### static

后期静态绑定,取初始调用类

    
```php
    class A {
        public static function who() {
            echo __CLASS__ . PHP_EOL;
        }
        public static function test() {
            static::who(); // 后期静态绑定从这里开始
        }
    }
    
    class B extends A {
        public static function who() {
            echo __CLASS__ . PHP_EOL;
        }
    }

    B::test();// 输出  B

```
    
    
    