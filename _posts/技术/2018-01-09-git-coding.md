---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/coding.jpg
date: 2018-01-09 15:54
title: 使用Git和Coding平台
category: 技术
ascription: technology
tags:
- Git
- 代码
---

个人比较喜欢使用git来上传代码，可以很方便的更新代码和进行回滚，一旦版本更新出Bug我可以借助Git的强大版本管理能力来修复Bug。
流程大概是这样：  
`本地代码－－－－>Coding－－－－>VPS`  
既然要使用git，那么先在VPS上安装git：  
`sudo apt-get install git`  
安装完成就可以使用git了，然后在Coding上创建一个私有项目laravel，里面包含所有该Laravel项目所需代码。  
## 本地代码推送到Coding
cd到项目目录下后：  
```
git init
git add .
git commit -m "init project"
git remote add origin https://coding.net//<项目名称>.git
git push origin master
```
首次提交至coding需要输入用户名&密码，直接输入即可。  
## 克隆到/var/www目录下
首先进入/var/www目录下，输入下面代码克隆：  
`git clone your-project-git-link`  
your-project-git-link替换为你Coding上的laravel项目地址。  
## 参考文章
[在Coding.net创建项目开发](http://www.jianshu.com/p/eaf2edb496f7)