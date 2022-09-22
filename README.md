
## myblog

*myblog* 用于记录一些坑，不断打脸，不断进步。

刷新认知。

## 新增文字方法

```shell
    ## 创建新文章
    hexo new title
    
    ## 新建about
    hexo new page "about"
    hexo new page "tags"
    hexo new page "categories"
    
    ## 创建文章 此处加了日期
    hexo new $(date +"%Y-%m-%d")."title"
    
    ## 发布
    hexo d -g
    
```

## 注意的⚠️
-       `##`   `###`  才展示目录

## 常见问题
remote: Support for password authentication was removed on August 13, 2021.

github 不支持账号密码提交了，需要生成个人token

## 生成index为空
 解决方式: 
    1. 升级hexo 版本
    2. 检查npm
 