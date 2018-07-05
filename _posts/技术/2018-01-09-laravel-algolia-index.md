---
layout: blog
istop: true
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/algolia.jpg
date: 2018-01-09 16:37
title: Laravel使用algolia的时，只添加一张表的部分字段到索引
category: 技术
ascription: technology
tags:
- Laravel
- 代码
---

最近在写文章的时候，总是出现提示algolia某个字段太大(too big)，分析之后发现algolia现在了字段的大小，像我这种使用免费版的，最大容量为10k，写篇长的文章轻易就超过了最大限度。 
![file](https://obdr74yw6.qnssl.com/image/77u25y8SjL3A6rO4TmdFlaa6PHEJI0FYQGy9vY7w.jpeg)  
怎么办呢？在这里我们在可以使用algolia的时候，可以只添加一张表的部分字段到索引。  
比如一张articles表，有下面这些字段：  
```
id title slug description content author status created_at updated_at deleted_at
```
我想只添加前面4个字段即id title slug description到索引，那么只需要这么操作即可。  
在你的 Article 这个 model 文件定义下面的方法：  
```
  public function toSearchableArray()
    {
       return [
           'id' => $this->id,
           'title' => $this->title,
           'slug' => $this->slug,
           'description' => $this->description
       ];
    }
```
里面的数组根据你的需求来定义可以了，而在实际操作中，搜索能够做到这样也是能满足需求的。