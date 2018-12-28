---
layout: blog
technology: true
background: green
background-image: /thumbs/ubuntu.jpg
date: 2018-01-08 18:12
title: Ubuntu下安装nodejs，npm
category: 技术
ascription: technology
tags:
- nodejs
- linux
---

# 前提
GCC 4.2 以上、G++ 4.2  以上、python2.7环境、wget 工具、make 工具

# 安装以上环境
`sudo apt-get install python gcc g++ wget make `  
在官网找到符合自己系统的源文件（source code），	官网地址：https://nodejs.org/en/download/ 。  
1. 	使用wget工具下载  
`wget https://nodejs.org/dist/v8.9.1/node-v8.9.1.tar.gz`  
2. 	解压  
`tar -zxvf node-v8.9.1.tar.gz  //注意下载.tar.gz`  
3.  进入解压文件，运行configure文件配置源代码  
`sudo ./configure`  
4.  使用make install 编译安装nodejs  
`sudo make install`  
5.  编译源文件需要一段时间，编译结束后，检查nodejs的版本号  
`node -v`  
如果能显示版本号，表明安装成功。  
nodejs安装的同时也安装了npm，检测npm版本号。  
npm安装的不一定是最新版本。  
npm -v      //检测版本号。  
`sudo npm  install -g npm` 　　//安装最新版本npm  

# 卸载node：（通过源文件编译安装的node）
```
1 进入安装时的源文件          cd  源文件
2 如果源文件不存在，下载一份，解压，进入源文件
3 
4 sudo make uninstall           //使用 make 卸载
5 进入/usr/local/lib/ 删除node_modules目录
6 在命令行输入 node -v 系统提示安装node
7 如果没有进入/usr/local/lib删除node_modules目录，执行node -v 时，系统提示在/usr/local/bin中无执行文件 
```