---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/2018/02/2813439775.png
date: 2018-03-02 16:46
title: 使用coding.net免费部署自己的PHP+Mysql网站并实现自定义域名和https服务
category: 技术
cslug: technology
tags:
- PHP
- Typecho
---

Coding.net 动态 Pages 是一个动态网页托管和演示服务，支持使用 PHP 语言和 MySQL 数据库，可用于部署开源博客、CMS 等动态应用。  

## 一、注册coding.net账户，新建自己的私有项目 ##  
登录网站[coding.net][1],点击右侧的注册按钮，注册一个自己的帐号，利用注册的帐号进入系统，为了使用pages功能+绑定自定义域名，最好进行完善资料认证升级为银牌会员。  
![coding会员](https://i.loli.net/2018/02/26/5a94256d5b1ab.png)  
从上面的会员体系可以看出，只有银牌以上的会员才可以实现本文的所有功能。  
完成之后，创建一个私有项目，进入刚刚创建的项目，点击左侧的代码——>代码浏览，可以看到新创建项目下的文件，点击代码——>Pages 服务，选中动态Pages，开启这个项目的Pages服务。此时已经为你生成一个网站地址，可点击浏览。    
![开启Pages服务](https://i.loli.net/2018/02/26/5a9428fd5cf3c.png)   
点击存储空间栏中的『连接信息』获取数据库连接信息。  
![数据库相关信息](https://i.loli.net/2018/02/26/5a942954893d8.png)  
注：数据库连接信息也可以通过环境变量方式获取，已经设置到了 $_ENV 里，分别是 MYSQL_DBNAME、MYSQL_USERNAME、MYSQL_PASSWORD、MYSQL_HOST、MYSQL_PORT。  

## 二、下载Git，并安装 ##  
下载安装Git可以参考[Windows Xampp 安装 Laravel及相关工具][2],这里的git是Windows下，故到这里[https://git-for-windows.github.io/][3] 下载exe文件安装即可。   

## 三、克隆新建的项目到本地 ##
在电脑上找个位置放自己项目代码，比如D盘根目录，那么进入D盘，右键选中Git Bash Here。
![Git Bash](https://i.loli.net/2018/02/26/5a942b15ccedd.png)  
打开了git命令框，clone你在coding.net上刚刚创建的项目。
项目地址在下图位置：  
![项目地址](https://i.loli.net/2018/02/26/5a942cd2471f0.png)  
在Git bash中输入命令克隆项目到本地：  
`git clone 上面这个地址`  
那么以你刚刚创建的项目名为目录的文件夹就创建好，cd 项目命，进入文件夹。

## 四、上传自己的网站程序到项目，mysql导入数据 ##  
将自己开发好的PHP网站程序到D盘下的项目文件夹里面，使用git命令上传代码到coding上。
```
git add ./ 
git commit -m "备注"
git push
```  
每条命令的作用自己去网上搜索。  
![重新部署](https://i.loli.net/2018/02/26/5a942e90033ac.png)  
上传完成后，将进行重新部署，这是自动的，你可以关闭自动部署功能。  
点击连接信息的phpMySQLAdmin,打开数据库管理后台，用户名和密码可以在左侧的连接信息按钮获取。  
![数据库相关信息](https://i.loli.net/2018/02/26/5a942954893d8.png)  
在程序里面涉及到数据库连接也需要做相应的修改。
进入数据库后台后，可以导入数据，至此，网站基本部署完成，可以使用开启Pages服务时生成的地址进行访问了。  

## 五、绑定自己的域名并开启https服务 ##  
如果你是银牌以上的会员，可以绑定自己的域名，开启https服务等操作。
这里有[自定义域名的帮助信息][4],操作也是很简单，先进域名解析里面绑定CNAME，接着输入域名绑定，还可以选择那个地址为首页，怎么跳转等，我的设置最后是这样的。  
![绑定域名](https://i.loli.net/2018/02/27/5a9430417f64d.png)  
开启https服务也很简单。  
![开启https服务](https://i.loli.net/2018/02/27/5a94308698490.png)  
可以选择强制开启。
在浏览器中输入网站[https://pangsuan.com][5]访问试试吧~~
![胖蒜网](https://i.loli.net/2018/02/27/5a9432b40c3f3.png)


  [1]: https://coding.net
  [2]: https://pangsuan.com/p/windows-laravel-deploy.html
  [3]: https://git-for-windows.github.io/
  [4]: https://coding.net/help/doc/pages/domain.html
  [5]: https://pangsuan.com