---
layout: blog
technology: true
background: blue
background-image: /thumbs/typecho.png
date: 2018-02-08 15:55
title: typecho在文章中插入广告
category: 技术
ascription: technology
tags:
- PHP
- Typecho
---

文章前面，最后插入广告太简单，那么怎么在文章中间插入广告呢，其实就是判断查找文章的第一个p，然后，插入代码，放到functions里使用即可。
![typecho-advertisement.jpg][1]
```
function themeInit($archive) {
    // 判断是否是文章，如果是就插入广告
    $ad_code = '<div>这是你的广告</div>';
    if ($archive->is('single')) {
        $archive->content = prefix_insert_after_paragraph( $ad_code, 2, $archive->content );;
    }
}
 
// 插入广告所需的功能代码
function prefix_insert_after_paragraph( $insertion, $paragraph_id, $content ) {
    $closing_p = '</p>';
    $paragraphs = explode( $closing_p, $content );
    foreach ($paragraphs as $index => $paragraph) {
        if ( trim( $paragraph ) ) {
            $paragraphs[$index] .= $closing_p;
        }
        if ( $paragraph_id == $index + 1 ) {
            $paragraphs[$index] .= $insertion;
        }
    }
    return implode( '', $paragraphs );
}
```

  [1]: https://obdr74yw6.qnssl.com/2018/02/401486379.jpg