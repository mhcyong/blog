---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/1506928035.jpg
date: 2018-01-09 16:21
title: Ubuntu下安装PhpStorm软件
category: 技术
tags:
- PHP
- 软件
---

PhpStorm 是 JetBrains 公司开发的一款商业的 PHP 集成开发工具，旨在提高用户效率，可深刻理解用户的编码，提供智能代码补全，快速导航以及即时错误检查。  
![file](https://obdr74yw6.qnssl.com/image/Izky2xomHrNMnzdBG15DYg52hEkIFeTRhdhLmD79.png)  
phpstorm是用JAVA开发的，所以在安装之前需要先安装jdk  
`sudo apt-get install default-jdk`  
## 从官网上下载phpstorm 的linux版本
http://www.jetbrains.com/phpstorm/download/index.html
## 解压压缩文件
`tar xfz PhpStorm-*.tar.gz`
## 进入phpstorm的bin目录执行安装脚本
`cd PhpStorm-* ./PhpStorm.sh`  
安装程序开始启动，在安装过程中需要输入注册码（可选）  
这里提供一种激活方式：  
开phpstorm软件选择License server选项填写http://www.imsxm.com/ ，然后点击Activate。

## 注意：
phpstorm7,8要求jdk 6以上版本，ubuntu默认安装jdk6 可以通过下面的方式安装：  
`sudo add-apt-repository ppa:webupd8team/java sudo apt-get update sudo apt-getinstall oracle-java7-installer`