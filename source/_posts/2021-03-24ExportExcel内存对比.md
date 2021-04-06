---
title: ExportExcel 内存对比
date: 2021-03-24 10:14:34
tags: PHP
---

### php使用excel组件

- Maatwebsite\Excel
- todo

###  大文件导出需设置内存


```php
     // 设置不限制内存
     ini_set('memory_limit', -1);

 
     echo "本次程序占用内存:" . $this->memory_usage();

     function memory_usage() {
            $memory  = ( ! function_exists('memory_get_usage')) ? '0' : round(memory_get_usage()/1024/1024, 2).'MB';
            return $memory;
      }


```


###  excel导出两种格式导出占用内存使用分布情况
  
 
     | 数量    |  xlsx    |  csv |  预计提升 |
     | ---- | ---- | ----- | ---- |
     | 1000   | 27.34MB  | 25.12MB  | ~~8.1%|
     | 10000  | 54.23MB  | 47.98MB  | ~~13%|
     | 100000 | 309.1MB  | 256.88MB | ~~16.9%|