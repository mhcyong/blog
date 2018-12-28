---
layout: blog
technology: true
background: blue
background-image: /thumbs/php.png
date: 2018-01-09 15:54
title: PHP获取网站中各文章的第一张图片的代码示例
category: 技术
ascription: technology
tags:
- PHP
- 图片
---

调取文章中的第一张图作为列表页缩略图是很流行的做法,WordPress中一般主题默认也是如此,那我们接下来就一起来看看PHP获取网站中各文章的第一张图片的代码示例。  
```
<?php 
$pattern="/<[img|IMG].*?src=[\'|\"](.*?(?:[\.gif|\.jpg|\.png]))[\'|\"].*?[\/]?>/"; 
$content = $article->Content; //文章内容 
preg_match_all($pattern,$content,$matchContent); 
if(isset($matchContent[1][0])){ 
  $temp=$matchContent[1][0]; 
}else{ 
  $temp="./images/no-image.jpg";//在相应位置放置一张命名为no-image的jpg图片 
} 
?>
```
调用文章首张图片，如果文章没有图片就调用默认图片no-image.jpg。