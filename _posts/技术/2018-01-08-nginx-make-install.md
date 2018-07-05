---
layout: blog
istop: true
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/nginx.jpg
date: 2018-01-08 23:00
title: Nginx手动安装、增加ssl模块、升级更新、删除等操作
category: 技术
ascription: technology
tags:
- linux
- Nginx
---

# 以下的操作都在Ubuntu系统下，其它系统请绕过
一般我们都需要先装pcre, zlib，前者为了重写rewrite，后者为了gzip压缩。  
```
sudo apt-get install libpcre3 libpcre3-dev        //PCRE库
sudo apt-get install zlib1g-dev                        //zlib库
sudo apt-get install openssl libssl-dev            //OpenSSL库
```
# 1.选定源码目录
选定目录 /usr/local/  
`cd /usr/local/`
 
# 2.安装nginx
Nginx 一般有两个版本，分别是稳定版和开发版，您可以根据您的目的来选择这两个版本的其中一个，下面是把 Nginx 安装到 /usr/local/nginx 目录下的详细步骤：
备注：nginx请到http://nginx.org/download 查找并下载。
 ```
cd /usr/local/
wget http://nginx.org/download/nginx-1.2.8.tar.gz
tar -zxvf nginx-1.2.8.tar.gz
cd nginx-1.2.8  
./configure --prefix=/usr/local/nginx 
make
make install
```
--with-pcre=/usr/src/pcre-8.21 指的是pcre-8.21 的源码路径。  
--with-zlib=/usr/src/zlib-1.2.7 指的是zlib-1.2.7 的源码路径。
 
# 3.启动
确保系统的 80 端口没被其他程序占用，  
`/usr/local/nginx/sbin/nginx`
检查是否启动成功：  
`netstat -ano|grep 80` 有结果输入说明启动成功  
打开浏览器访问此机器的 IP，如果浏览器出现 Welcome to nginx! 则表示 Nginx 已经安装并运行成功。
 
# 4.重启
`/usr/local/nginx/sbin/nginx –s reload`
 
# 5.修改配置文件
```
cd /usr/local/nginx/conf
vi nginx.conf
```

# 6、增加未开启的ssl，http2模块
切换到源码包`cd /usr/local/nginx-1.2.8`后查看nginx原有的模块  
`sudo /usr/local/nginx/sbin/nginx -V`  
原有应该如下：  
`--prefix=/usr/local/nginx `  
新的配置应该这么写：  
`--prefix=/usr/local/nginx  --with-http_ssl_module  --with-http_v2_module `  
那么应该运行下面的命令，配置完成后，执行：  
`./configure --prefix=/usr/local/nginx  --with-http_ssl_module  --with-http_v2_module `  
配置完成后，运行命令：
`make`  
不要make install，否则就覆盖安装了。  
先停止nginx运行`pkill -9 nginx`，这里强制停止。  
然后备份原有已经安装好的nginx配置  
`cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak`  
将刚刚编译的覆盖原有的nginx  
`cp ./objs/nginx  /usr/local/nginx/sbin/`  
启动nginx:  
`/usr/local/nginx/sbin/nginx`  
查看是否安装成功新的ssl模块：  
`sudo /usr/local/nginx/sbin/nginx -V`  

# 7、升级nginx
下载最新版nginx源码并解压编译  
```
cd /usr/local/
wget http://nginx.org/download/nginx-1.13.6.tar.gz
tar zxvf nginx-1.13.6.tar.gz
cd nginx-1.13.6
#编译nginx，添加http_v2模块应用
```
开始编译nginx  
`./configure --prefix=/usr/local/nginx   --with-http_ssl_module  --with-http_v2_module`  
编译完成后，执行make，但不执行make install  
`make`  
将旧版本的nginx二进制文件，重命名一个名字，在这期间，当前运行的nginx进程不会停止，不影响应用运行。  
`mv /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.old`  
然后将上一步通过make编译好的新版nginx二进制文件，拷贝到运行目录  
`cp ./objs/nginx /usr/local/nginx/sbin/nginx`  
在源码目录根目录下，执行更新安装命令:  
`make upgrade`  
注意：如果原来的相关配置文件中，写有和ssl有关的配置信息，需要先暂时注释掉，否则更新时会报错。  
更新完成后，执行  
`nginx -V`  
可以看到nginx已经更新到1.13.6版本。  

# 8、参考地址
1、https://www.cnblogs.com/ghjbk/p/6744131.html
2、[Nginx的SSL配置优化](https://www.linpx.com/p/ssl-configuration-optimization.html)
3、[ ubuntu下安装nginx时PCRE库、zlib库、OpenSSL库的安装](http://blog.csdn.net/somanlee/article/details/69808788)
4、[nginx支持HTTP2的配置过程](https://www.cnblogs.com/bugutian/p/6628455.html)
5、[Mozilla SSL Configuration Generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
6、[ubuntu 16.04.1 nginx彻底删除](http://blog.csdn.net/fg_411/article/details/54928159)