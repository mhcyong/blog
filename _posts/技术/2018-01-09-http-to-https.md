---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/1505924714.jpg
date: 2018-01-09 15:54
title: http跳转到https，并优化SSL
category: 技术
cslug: technology
tags:
- SSL
- https
---

这里，我们是在Nginx里面配置的，编程语言使用的PHP，当然你也可以用其它语言，但是Nginx下SSL配置是本文的讲点。  
![](https://obdr74yw6.qnssl.com/https.jpg)  
首先，请确保安装了openssl，接着执行:  
`sudo openssl dhparam -out /etc/nginx/ssl/dhparam.pem 2048`  
接着打开下面网址  
https://mozilla.github.io/server-side-tls/ssl-config-generator/  
Server Version   通过`nginx -v`查找  
OpenSSL Version  通过 `openssl version -a`查找  
HSTS Enabled 启用  
将生产的配置拷贝到/etc/nginx/sites-avilable/default里面，SSL证书可以到下面申请免费的。  
1、https://letsencrypt.org/  
2、https://www.sslforfree.com/  
将生成证书放在 /etc/nginx/ssl/目录下，修改上面配置中相应地址即可。  
如果没有什么大问题，应该是A+了吧。  
还有一个叫Certbot的工具，可以试试，很方便的。