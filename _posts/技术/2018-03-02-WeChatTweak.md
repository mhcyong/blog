---
layout: blog
istop: true
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/2018/03/1324646771.png
date: 2018-03-02 08:34
title: WeChatTweak – 支持「防撤回」与「多开」的微信 macOS 客户端
category: 技术
tags:
- macOS
- 微信
---

WeChatTweak 是一款支持「防撤回」与「多开」的微信 macOS 客户端第三方插件，并且还拥有「免手机认证登录」等功能。  
![WeChatTweak-macOS](https://i.loli.net/2018/03/02/5a989b68e70f8.jpg)  
WeChatTweak 并不是一个独立的客户端，而是一款插件，目前仅支持 macOS，并且需要首先安装微信 for Mac 官方客户端。  
之后需要使用命令行来安装 WeChatTweak，方法如下：  

打开终端（Terminal）  
下载源码：  `git clone https://github.com/Sunnyyoung/WeChatTweak-macOS.git`  
进入目录：  `cd WeChatTweak-macOS`  
编译安装：  `sudo make install`  
打开微信客户端  

卸载请使用命令行：  `sudo make uninstall`  

最终，WeChatTweak 将实现以下几个非常实用的功能：  

阻止消息撤回  
消息列表通知  
系统通知  
正常撤回自己发出的消息  
客户端无限多开  
右键 dock icon 登录新的微信账号  
命令行执行：  `open -n /Applications/WeChat.app`  
重新打开应用无需手机认证  
UI界面设置面板  
然后，就可以愉快的玩耍了。  