---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/image/FEnRv5j8yFuhN57kGtdQBCc69YMgSq0knUZwGQes.png
date: 2018-01-08 18:16
title: Windows Xampp 安装 Laravel及相关工具
category: 技术
cslug: technology
tags:
- PHP
- Lavarel
---

# 前提
开始之前，目前使用的 Laravel 主流版本大概需要以下依赖：  
1. PHP >= 5.6.4  
2. PHP OpenSSL 扩展  
3. PHP PDO 扩展  
4. PHP Mbstring 扩展  
5. PHP Tokenizer 扩展  
6. PHP XML 扩展  

注意的是，Laravel 5.5 据说是直接要求 PHP 7.0 以上了。  
# 安装 Xampp
这个就很简单啦！  
从这里：https://www.apachefriends.org/zh_cn/index.html 下载安装文件，双击运行，点击下一步，下一步就可以。  
![Xampp](https://obdr74yw6.qnssl.com/image/VkeqUoTSbLtDT2iDcSGJVpvQGA1nVLno2esi5QrJ.png)
你可以看到我们安装的是 PHP7.1 的版本，所以不用担心这个问题。  
安装完成后是这样的：
![Xampp](https://obdr74yw6.qnssl.com/image/FEnRv5j8yFuhN57kGtdQBCc69YMgSq0knUZwGQes.png)  
点击需要的功能启用即可。

# 安装 Composer
安装 Composer 其实也是一样的简单，这里： https://getcomposer.org/download/  
下载。双击安装就好。（注意一下网络就好，这个自己想办法）  
安装之后，你可以得到一个可执行的 composer 命令，为了达到更好的体验，文章最后会讲解Git的使用。

# 配置 Xampp Virtual Host
如果你没做任何改动，Xampp 的配置文件大概是在 C:\xampp\apache\conf\extra\httpd-vhosts.conf 这个位置。在这个文件里面，我们可以添加以下代码：  
```
<VirtualHost laravel.dev:80>
  DocumentRoot "C:\xampp\htdocs\laravel\public"
  ServerAdmin laravel.dev
  <Directory "C:\xampp\htdocs\laravel">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
  </Directory>
</VirtualHost>
```
注意 DocumentRoot 和 Directory 的设置。  
# 添加 hosts
hosts 文件在 Windows 上通常是位于 C:\Windows\System32\drivers\etc 这个文件夹里面，编辑 hosts 文件添加下面这一行：
```
127.0.0.1    laravel.dev
```
如果你没有权限编辑的话（通常要管理员身份运行），右键，选择属性，选择该用户修改

# 安装 Laravel
直接使用 Composer 来安装就好：  
`composer create-project --prefer-dist laravel/laravel laravel`  
注意这里运行这行命令需要在对应的 C:\xampp\htdocs\ 目录下，因为这个目录是我们在配置 Xampp 的 Virtual Host 目录啊。  
等待安装完毕。（网络问题自己解决哦）浏览器访问 laravel.dev 应该就 OK 了！

# 安装phpstorm
PhpStorm 是 JetBrains 公司开发的一款商业的 PHP 集成开发工具，旨在提高用户效率，可深刻理解用户的编码，提供智能代码补全，快速导航以及即时错误检查。  
[http://www.jetbrains.com/phpstorm/download/index.html](http://www.jetbrains.com/phpstorm/download/index.html)
打开phpstorm软件选择License server选项填写http://www.imsxm.com/ ，然后点击Activate激活。  
![安装phpstorm](https://obdr74yw6.qnssl.com/image/pP01BcL8HXCulIEoehZTFUiz6lutq2cKB4ZWIXlB.png)

# 安装git
这里的git是Windows下，故到这里https://git-for-windows.github.io/ 下载exe文件安装即可。  
安装完成后，在 C:\xampp\htdocs\ 目录下右键选择Git GUI Here，在打开的gitbash里面，输入composer,显示如下即表示一切安装成功。
![安装git](https://obdr74yw6.qnssl.com/image/t4IdY086WJlV4cmllGI7hyuW5YIjHjpUOWPPMsTv.png)