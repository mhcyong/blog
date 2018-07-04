---
layout: blog
technology: true
background: yellow
background-image: https://obdr74yw6.qnssl.com/laravel5.jpg
date: 2018-01-09 15:54
title: Ubuntu下创建Laravel项目
category: 技术
tags:
- PHP
- Laravel
---

我们建议通过Composer来安装Laravel，方便以后的管理，还有在开发过程中需要使用一些依赖包，使用Composer将让你的开发更简单快捷。  
在《[Ubuntu下安装并配置PHP7+MySQL+Nginx+SSL网站环境](https://pangsuan.com/p/Ubuntu-PHP-MySQL-Nginx-SSL.html)》中，我们已经配置好了PHP开发环境，下面我们来创建laravel项目。  
## composer安装
在《[如何安装 Composer（国内镜像）](https://pangsuan.com/p/composer-ghost.html)》已经讲解了如何安装，当然你也可以在[Composer官网](https://getcomposer.org/download/)了解如何安装：  
```
sudo apt install curl
curl -sS https://getcomposer.org/installer | php
php composer.phar    //测试是否安装成功
```
之后我建议全局安装：  
`sudo mv composer.phar /usr/local/bin/composer`
## Laravel安装
在/var/www目录下直接执行：  
`sudo composer create-project laravel/laravel laravel`  
因为我们之前创建/var/www目录，你可以直接cd /var/www然后执行上面的命令，然后坐等安装完成。  
## 权限和访问限制
不管哪种方式安装的代码，/var/www/都是属于root用户的，而访问网站的用户则需要正确的权限和访问限制，我们可以通过下面的命令来实现。  
`sudo chown -R :www-data /var/www/laravel`  
根据Laravel的官方文档，`/var/www/laravel/storage` 目录需要给网站的用户写权限。  
`sudo chmod -R 775 /var/www/laravel/storage` 
## 访问网站
在浏览器输入：  
http://your-ip-address  
![Laravel5](https://obdr74yw6.qnssl.com/image/mwq28AxIfM31l3JzqDFF7mDjxueBAHCbE3E3YmHT.png)  
或者cd 到/var/www/laravel，  
### 方法一
命令行输入：`php artisan serve`，在浏览器输入http://your-ip-address:8000 访问。
### 方法二
命令行输入：`php -S localhost:8888 -t public`，在浏览器输入http://your-ip-address:8888 访问。
至此，整个Laravel项目创建成功，开始享用吧。