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
     
###  字节和内存大小

①ASCII码中，一个英文字母（不分大小写）占一个字节的空间，一个中文汉字占两个字节的空间。一个二进制数字序列，在计算机中作为一个数字单元，一般为8位二进制数，换算为十进制。最小值0，最大值255。
②UTF-8编码中，一个英文字符等于一个字节，一个中文（含繁体）等于三个字节。
③Unicode编码中，一个英文等于两个字节，一个中文（含繁体）等于两个字节。



预计占用内存计算：
       字节       kb     mb
1000000 * 20  / 1024 / 1024  = 19M


```
   1B（Byte字节）=8bit
　　1KB (Kilobyte 千字节)=1024B，
　　1MB (Mega byte 兆字节 简称“兆”)=1024KB，
　　1GB (Giga byte 吉字节 又称“千兆”)=1024MB，
　　1TB (Tera byte 万亿字节 太字节)=1024GB，其中1024=2^10 ( 2 的10次方)   
```  