---
title: 建立composer包的过程
date: 2019-02-28 17:04:52
tags: composer
---


1. 在github 创建文件仓库 如：https://github.com/caijihui/computeman.git

2. 下载到本地，进行基础构建
```bash
     git clone https://github.com/caijihui/computeman.git
     composer init 
     ## 建立好composer.json 后运行，下载依赖 
     composer install
```
  **composer.json 参考文件**
 ```json
  {
      "name": "xxx/xxx",
      "description": "xx",
      "keywords": [
          "laravel",
          "compute",
          "age"
      ],
      "require": {
          "php": ">=7"
      },
      "autoload": {
          "psr-4": {
              "aaa\\": "src/"
          }
      },
      "license": "MIT",
      "authors": [
          {
              "name": "aaaaa",
              "email": "aaaaaa@163.com"
          }
      ],
      "minimum-stability": "dev"
  }

 ```
3.目录结构如下,readme.md 补充使用流程
   ```file
        .git/  
        .gitignore  
        composer.json  
        README.md  
        src/
            compute.php  
   ```
 
4.编写代码进行本地测试
 
5.在根目录下建立个demo.php
   ```php
        require_once './vendor/autoload.php';
        use Computeman\Compute;
        
        echo Compute::getAge('1990-02-15');
   ```
   
6.测试通过之后，提交到github打上tag

**这里的tag 为composer包的版本**

命令参考：
```bash
            git tag v1.0
            git push origin v1.0
            ## 删除tag命令  
            git tag -d v1.0
            ## 删除远程tag
            git push origin --delete tag v1.0
```
7.到https://packagist.org/packages/submit 输入url 提交发布

8.正式使用,ok
```sh
    composer require caiyuanzi/computeman v1.0  
```
