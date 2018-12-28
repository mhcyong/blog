---
layout: blog
technology: true
background: orange
background-image: /thumbs/php.png
date: 2018-01-09 16:26
title: PHP生成八位随机字符串
category: 技术
ascription: technology
tags:
- PHP
- 代码
---

```php
<?php  
// 当前的毫秒时间戳  
function msectime(){  
    $arr = explode(' ', microtime());  
    $tmp1 = $arr[0];  
    $tmp2 = $arr[1];  
    return (float)sprintf('%.0f', (floatval($tmp1) + floatval($tmp2)) * 1000);  
}  
// 10进制转62进制  
function dec62($dec){  
    $base = 62;  
    $chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';  
    $ret = '';  
    for($t = floor(log10($dec) / log10($base)); $t >= 0; $t--){  
        $a = floor($dec / pow($base, $t));  
        $ret .= substr($chars, $a, 1);  
        $dec -= $a * pow($base, $t);  
    }  
    return $ret;  
}  
// 随机字符  
function rand_char(){  
    $base = 62;  
    $chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';  
    return $chars[mt_rand(1, $base) - 1];  
}  
$str_time = dec62(msectime());  
// 8位随机字符串  
$code = rand_char().$str_time;  
var_dump($code); 
```