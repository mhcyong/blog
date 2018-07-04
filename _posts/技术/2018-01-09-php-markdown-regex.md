---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/markdown.jpg
date: 2018-01-09 15:54
title: 正则匹配Markdown的图片地址
category: 技术
tags:
- PHP
- Markdown
---

使用PHP提取Markdown图片的正则如下：
`$pattern = '/!\\[.*\\]\\((.+)\\)/';`