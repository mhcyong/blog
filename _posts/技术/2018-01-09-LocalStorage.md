---
layout: blog
technology: true
background: yellow
background-image: https://obdr74yw6.qnssl.com/1506671773.jpg
date: 2018-01-09 16:34
title: LocalStorage 本地存储解决方案及应用实例
category: 技术
ascription: technology
tags:
- session
- local
---

WEB应用的快速发展，是的本地存储一些数据也成为一种重要的需求，实现的方案也有很多，最普通的就是cookie了，大家也经常都用，但是cookie的缺点是显而易见的，其他的方案比如：IE6以上的userData，Firefox下面的globalStorage，以及Flash的本地存储，除了Flash之外，其他的几个都有一些兼容性的问题。  
![file](https://obdr74yw6.qnssl.com/image/026Tz7LygCtxoWLlC3D4dDpcKjY7h6Smk5ypLBkV.jpeg)  
## sessionStorage与localStorage
1、Web Storage实际上由两部分组成：sessionStorage与localStorage。 
2、sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并3、且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。  
localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。  
## 浏览器支持
Internet Explorer 8+, Firefox, Opera, Chrome, 和 Safari支持Web 存储。  
注意: Internet Explorer 7 及更早IE版本不支持web 存储。  
## 检测浏览器是否支持本地存储
在HTML5中，本地存储是一个window的属性，包括localStorage和sessionStorage，从名字应该可以很清楚的辨认二者的区别，前者是一直存在本地的，后者只是伴随着session，窗口一旦关闭就没了。二者用法完全相同，这里以localStorage为例。  
```
if(window.localStorage){
 alert('This browser supports localStorage');
}else{
 alert('This browser does NOT support localStorage');
}
```
## 存储数据的方法
直接给window.localStorage添加一个属性，例如：window.localStorage.a 或者 window.localStorage["a"]。它的读取、写、删除操作方法很简单，是以键值对的方式存在的，如下：  
```
localStorage.a = 3;//设置a为"3"
localStorage["a"] = "sfsf";//设置a为"sfsf"，覆盖上面的值
localStorage.setItem("b","isaac");//设置b为"isaac"
var a1 = localStorage["a"];//获取a的值
var a2 = localStorage.a;//获取a的值
var b = localStorage.getItem("b");//获取b的值
localStorage.removeItem("c");//清除c的值
```
## 实际应用
首先插入这段js代码：  
```
    <script type="text/javascript">
       if(window.localStorage){
           var storage=window.localStorage;
           //获取文本框值并保存
           function getValue() {
               var inputEle = document.getElementById("txtContent").innerHTML;
               storage.newpost=inputEle;
           }
           //获取保存值到文本框
           if(storage.newpost){
               $(document).ready(function () {
                   document.getElementById("txtContent").value=storage.newpost;
               });
           }
       }else{
           alert("浏览器不支持本地存储");
       }
    </script>
```
其次在你要保存的文本框调用这个函数，这里实现了实时保存。  
```
 <textarea id="txtContent" name="content"  onkeyup="getValue();"></textarea>
```