---
layout: blog
technology: true
background: res
background-image: https://obdr74yw6.qnssl.com/html5-css3.jpg
date: 2018-01-09 16:35
title: 用CSS让字体在一行内显示不换行
category: 技术
cslug: technology
tags:
- CSS
- 代码
---

当一行文字超过DIV或者Table的宽度的时候，浏览器中默认是让它换行显示的，如果不想让他换行要怎么办呢？  
一般的文字截断(适用于内联与块)：  

```css
.text-overflow{
	display:block;                     /*内联对象需加*/
	width:31em;
	word-break:keep-all;           /* 不换行 */
	white-space:nowrap;          /* 不换行 */
	overflow:hidden;               /* 内容超出宽度时隐藏超出部分的内容 */
	text-overflow:ellipsis;         /* 当对象内文本溢出时显示省略标记(...) ；需与overflow:hidden;一起使用。*/
}
```

对于表格，定义有点不一样：  

```css
table{
	width:30em;
	table-layout:fixed;                 /* 只有定义了表格的布局算法为fixed，下面td的定义才能起作用。 */
}
td{
	width:100%;
	word-break:keep-all;             /* 不换行 */
	white-space:nowrap;            /* 不换行 */
	overflow:hidden;                  /* 内容超出宽度时隐藏超出部分的内容 */
	text-overflow:ellipsis;            /* 当对象内文本溢出时显示省略标记(...) ；需与overflow:hidden;一起使用。*/
}
```

注：这个只对单行的文字的效，如果你想把它用在多行上，也只有第一行有作用的。 这个写法只有IE会有“...”，其它的浏览器文本超出指定宽度时会隐藏。