---
layout: blog
technology: true
background: red
background-image: /thumbs/ubuntu.png
date: 2018-01-09 16:28
title: Ubuntu下客户端配置Shadowsocks
category: 技术
ascription: technology
tags:
- 软件
- linux
---

# 1、安装 shadowsocks 客户端  
ss 的客户端有很多语言实现，包括 Python、Go、libev等，这里使用广泛的 Python 后端。  
```
sudo apt-get update  
sudo apt-get install python-pip    
sudo pip install shadowsocks  
```
此时系统会多出来两个程序：  
```
/usr/bin/ssserver  
/usr/bin/sslocal  
```
# 2、配置shadowsocks
`sudo vim /etc/shadowsocks.json  `  
然后会跳出一个文本框，粘贴以下内容  
```
{  
    "server":"xx.xx.xx.xx",  
    "server_port":xxxx,  
    "local_address": "127.0.0.1",  
    "local_port":1080,  
    "password":"xxxxxxxx",  
    "timeout":300,  
    "method":"aes-256-cfb",  
    "fast_open": true,  
    "workers": 1  
}  
```
# 3、启动shadowsocks
`sudo sslocal -c /etc/shadowsocks.json`  
这样，shadowsocks就运行了。但怎么通过它上网呢，这就要设置浏览器了。下面介绍chrome浏览器的设置。

# 4、chrome浏览器，代理设置
    4.1、点击浏览器右上角三个点，“更多工具”，"扩展程序"，“获取更多扩展程序”，搜索“proxy switchysharp”，下载安装  
    4.2、然后打开 Proxy SwitchySharp 的设置，新建一个情景，命名为 Shadowsocks，并设置好端口，模式为 socks5 如图：  
![file](https://obdr74yw6.qnssl.com/image/AquxWXck4IUn4K5G42dqDuyo420aeYWHXh7novjf.jpeg)  
再点切换规则，由于可能大概无法访问 Google，我们就启用切换规则，然后在 URL 模式里输入 *google* 统配好 Google 的所有域名，选择好模式匹配为通配符，情景模式为 Shadowsocks  
然后把在线规则列表打钩，输入 URL 为：  
`https://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt`  
勾选 AutoProxy 兼容列表，然后点立即更新，更新完成后保存即可，如图：  
![file](https://obdr74yw6.qnssl.com/image/9ZR3tUTKd7WCSJnttnEpas0KsqxIT5N0sLWIOl0P.jpeg)  
# 5、配置开机启动
`sudo vim  /etc/rc.local`  
在exit0上一行加上/usr/local/bin/sslocal -c /etc/shadowsocks.json -d start  

# 6、Ubuntu下配置全局代理上网
Setting->network->Network proxy设置方法为Manual，如下图所示：  
![file](https://obdr74yw6.qnssl.com/image/VdtNuQsOz0e4GKJJvD3l6yPIQmhKrtutfNWtV0cy.png)  
点击Apply system wide即设置完成全局上网代理。  

# 7、参考文章
1）[ubuntu下配置shadowsock](http://blog.csdn.net/scut_hy/article/details/52691649)  
2）[科学上网利器 Shadowsocks 使用方法](https://ttt.tt/150/)  
3）[使用shadowsocks轻松搭建翻墙环境教程](https://blog.phpgao.com/shadowsocks_on_linux.html) 