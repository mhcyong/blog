---
layout: blog
istop: true
technology: true
background: blue
background-image: https://obdr74yw6.qnssl.com/follow-fixed.jpg
date: 2018-01-09 16:36
title: 提高浏览量的特效：侧栏跟随滚动条
category: 技术
ascription: technology
tags:
- CSS
- 代码
---

现在许多web2.0风格的网站都喜欢用“侧栏跟随”的效果，就是当一个页面很长的时候，设定侧栏内容会跟随滚动条，这种效果适用于评论较多、内容较长的网站。
这种特效对提高网站浏览量、文章点击率、广告点击量都有一定效果。
**CSS部分：**
```css
/*侧栏跟随*/
#box{float:left; position:relative;width:250px;}  
.div1{width:250px;}  
.div2{position:fixed;_position:absolute;top:0;z-index:250;}
```
注：每个网站的侧栏宽度不同，可根据你网页的宽度调整div1的宽度，我的是width:250px;，把这段代码添加到你的CSS文件中即可。

**JS部分：**
```javascript
//侧栏跟随
(function(){
   var oDiv=document.getElementById("float");
   var H=0,iE6;
   var Y=oDiv;
   while(Y){H+=Y.offsetTop;Y=Y.offsetParent};
   iE6=window.ActiveXObject&&!window.XMLHttpRequest;
   if(!iE6){
       window.onscroll=function()
       {
           var s=document.body.scrollTop||document.documentElement.scrollTop;
           if(s>H){oDiv.className="div1 div2";if(iE6){oDiv.style.top=(s-H)+"px";}}
           else{oDiv.className="div1";}    
       };
   }
})();
```

**网页代码部分：**
```
<div id="box">
<div id="float" class="div1"> 

这里写你网站的代码与标签。

</div>
</div>
```

特别提示：此代码试用于任何CMS系统，但该特效在IE6下无法实现，其余浏览器均没问题，同时侧栏其余部分应使用静态文件调用，使用JS调用栏目会出现代码重叠现象，调用联盟广告没问题。