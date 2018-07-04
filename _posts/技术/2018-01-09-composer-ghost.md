---
layout: blog
technology: true
background: orange
background-image: https://obdr74yw6.qnssl.com/1510826793.jpg
date: 2018-01-09 15:56
title: 如何安装 Composer（国内镜像）
category: 技术
tags:
- Lravel
- PHP
---

下载 Composer安装前请务必确保已经正确安装了 PHP。  
打开命令行窗口并执行 php -v 查看是否正确输出版本号。  
打开命令行并依次执行下列命令安装最新版本的 Composer：  
复制 `php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"`  
复制 `php composer-setup.php`  
复制 `php -r "unlink('composer-setup.php');"`  
![Composer](https://obdr74yw6.qnssl.com/59b5fea118371_25.jpg)  
执行第一条命令下载下来的 composer-setup.php 脚本将简单地检测 php.ini 中的参数设置，如果某些参数未正确设置则会给出警告；然后下载最新版本的 composer.phar 文件到当前目录。  
上述 3 条命令的作用依次是：  
1、下载安装脚本。  
2、执行安装过程。  
3、删除安装脚本。  
局部安装上述下载 Composer 的过程正确执行完毕后，可以将 composer.phar 文件复制到任意目录（比如项目根目录下），然后通过 php composer.phar 指令即可使用 Composer 了！  
全局安装全局安装是将 Composer 安装到系统环境变量 PATH 所包含的路径下面，然后就能够在命令行窗口中直接执行 composer 命令了。  
Mac 或 Linux 系统：打开命令行窗口并执行如下命令将前面下载的 composer.phar 文件移动到 /usr/local/bin/目录下面：  
 `sudo mv composer.phar /usr/local/bin/composer`   
Windows下安装更简单，下载exe文件，一路next即可。  
安装完成后，composer还是使用国外的镜像资源，这里推荐一个国内的镜像。  
打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：  
```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```
 即将配置信息添加到 Composer 的全局配置文件 config.json 中。  
最后重新打开一个命令行窗口试一试执行 composer --version 看看是否正确输出版本号。  
最后提示：不要忘了经常执行composer selfupdate 以保持 Composer 一直是最新版本哦！