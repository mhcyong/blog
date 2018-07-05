---
layout: blog
istop: true
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/image/kTi9qN8jgjR69nGeakwTrnL4lz8LD2vozYlArrpe.png
date: 2018-01-08 21:44
title: 解决vultr使用Snapshot快照恢复后没有root密码
category: 技术
ascription: technology
tags:
- linux
- VPS
---

首先你得有一台[vultr](https://www.vultr.com/?ref=7217973)的VPS，然后才可以看本文。
![vultr](https://obdr74yw6.qnssl.com/image/kTi9qN8jgjR69nGeakwTrnL4lz8LD2vozYlArrpe.png)  
本文适合Ubuntu、Debian系统用户。  
1、点击[View Console]进入系统登陆界面，点击右上角的CTRL+ALT+DEL按钮，当然你也可以点击 [RESTART] 重启服务器。  
2、当服务器开始重启时候，按下ESC按钮来到GRUB界面。  
3、当看到GRUB启动界面时候，按下键盘上的“e“，去编辑第一条启动信息。  
4、找到以"linux /boot/"开头的一行，在这行最后添加` init="/bin/bash" `。  
5、按下CTRL-X or F10去重启。  
6、系统将会重启，你将会看到root界面，输入`"mount -rw -o remount /"`，回车，然后输入`"passwd"`来更改root密码。  

其他系统或者更详细的资料请浏览：  
https://www.vultr.com/docs/boot-into-single-user-mode-reset-root-password