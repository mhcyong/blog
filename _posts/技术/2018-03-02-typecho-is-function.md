---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/2018/02/401486379.jpg
date: 2018-03-02 08:30
title: Typecho中的is函数
category: 技术
ascription: technology
tags:
- PHP
- Typecho
---

## 什么是is ##  
Typecho中内置了强大的is函数，用于判断“我在哪里？”。在制作主题页面的时候，经常需要根据页面的位置来加设特殊的效果，譬如在首页显示搜索框，但在归档页则显示最新评论：  
```
<?php if($this->is('index')): ?>
  <?php $this->need('search_box.php');?>
<?php else: ?>
  <?php $this->need('comment_section.php');?>
<?php endif;?>
```  
## is真面目 ##  
/var/Widget/Archive.php中，Widget_Archive类定义了我们所使用的is函数，原型如下：  
```
/**
 * 判断归档类型和名称
 *
 * @access public
 * @param string $archiveType 归档类型
 * @param string $archiveSlug 归档名称
 * @return boolean
 */

public function is($archiveType, $archiveSlug = NULL)
{
    //Some code here...
}
```  
可见，is函数的第一个参数表示归档类型，第二个参数表示归档名称，其中第二个参数可选。  
## is可用于哪些判断？ ##  
is函数可以用于判断index/archive/category/tag/date/single/page/post/attachment等，具体用法见下文描述。注意哈，这些页面是有相互包含的关系的，具体在使用过程中要多尝试下。  
$this->is('index')  
从字面可见，判断当前页面是否是首页  
$this->is('archive')  
判断当前页面是否是归档页，譬如主页，分类文章页，标签文章页，日期归档文章页  
$this->is('category')，或者$this->is('category','some_slug')  
判断当前页面是否为分类文章页，如果加第二个参数slug，则进一步判断是否为特定的分类，譬如默认分类的slug是“default”  
$this->is('tag')或者$this->is('tag','some_slug')  
判断当前页面是否是标签文章页，如果加第二个参数slug，则进一步精确判断，原理同category  
$this->is('date')或者$this->is('date','some_range')，其中some_rage可以是year/month/day  
判断当前页面是否是日期归档页，如果指定第二个参数，则进一步精确判断。  
$this->is('single')  
用于判断是否是内容页面，所谓内容页面，包括文章页、独立页面和附件显示页  
$this->is('post')或者$this->is('post',$post_id)  
用于判断是否是内容页，加第二个参数则进行精确判断  
$this->is('page')或者$this->is('page','some_slug')  
用于判断当前页面是否为独立页面，加第二个参数表示精确判断，譬如$this->is('page','about')则表示判断当前页面是否是about页面  
$this->is('attachment')或者$this->is('attachment',$attachment_id)  
同上，用于判断附件页面。  