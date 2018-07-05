---
layout: blog
istop: true
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/image/x3msBA7Z5t0LUaWaJoUKvArQibFV0WT8Q6XGFzyG.jpeg
date: 2018-01-08 18:14
title: Window10  64bit下安装Golang语言，Git，gvt，Echo框架
category: 技术
ascription: technology
tags:
- Golang
- 代码
---

![Window10  64bit下安装Golang](https://obdr74yw6.qnssl.com/image/x3msBA7Z5t0LUaWaJoUKvArQibFV0WT8Q6XGFzyG.jpeg)

# 一、安装golang程序
既然是windows下，那么就用MSI包安装吧，国外不用去了，大部分人访问不了，那么就到这里，[https://studygolang.com/dl](https://studygolang.com/dl) ，下载安装包，一路NEXT下去，基本就安装在C盘的Go文件夹下了。  
这种安装应该也配置好了，那么win+R，输入cmd回车，输入go，看是否安装成功了。  

# 二、安装Git
既然是windows，那么就下载exe安装包，一路下去，应该就安装好了。

# 三、安装配置gvt
打开cmd命令控制行，输入：`go get -u github.com/FiloSottile/gvt`  
接下来开始配置了，系统高级，环境变量，GOPATH，变量值为：`C:\Users\Administrator\go`，可以先看看这个文件夹是否有gvt.exe文件，PATH里面增加`%GOPATH%\bin`。

# 四、安装echo框架
因为golang.org在我们伟大的天朝无法访问的原因，所以按照官网上面的介绍是万万不可能安装成功的，这里我来把我之前安装的步骤整理一下，自己整理的，难免有错，如果有问题请及时告知。  
我们在安装过程中遵循的原则就是缺什么组件就单独下载安装什么组件  
1. 先按照官网上面的操作步骤来安装 ` go get github.com/labstack/echo`，查看报错信息  
`package golang.org/x/crypto/acme/autocert: unrecognized import path "golang.org/x/crypto/acme/autocert"`  
2. 分析错误，如上图所示，我们缺少crypto组件，需要下载，使用`go get golang.org/x/crypto/acme/autocert`来下载，但是强大的防御网真不是盖的。提示`package golang.org/x/crypto/acme/autocert: unrecognized import path "golang.org/x/crypto/acme/autocert"`，意思是该域名无法被识别。  
3. 好吧，那咱们只能用半自动的方式安装了，golang.org在github.com上面有一个备份镜像，幸亏github没有被屏蔽，因此，缺少的组件我们可以在github上面下载。  
我们使用`https://github.com/golang/***`的形式访问所缺少的组件，目前我们先访问`https://github.com/golang/crypto`下载该组件。  
4. 根据安装echo框架的提示，我们需要将该组件安装至`$(GOROOT)/src/golang.org/x/`位置，文件夹名称为crypto,以我的主机为例，我的`C:\Go\src\golang.org\x\`位置，没有就手动创建文件夹。  
5. 继续安装echo ----  `go get github.com/labstack/echo/` , 报错信息如下    
`package golang.org/x/net/context: unrecognized import path "golang.org/x/net/context" `。  
6. 如法炮制，再次利用github下载该组件，网址是`https://github.com/golang/net `。  
7. 好了，需要的两个组件已经安装完了，最后一次使用`go get github.com/labstack/echo/ `安装echo框架，---- OK成功。  
8. 好了，开启你们的echo之旅吧，顺带说一句，以后再碰到无法安装`golang.org/x/***/`之类的错误，只需要到`https://github.com/golang/***`去下载，放到`${GOROOT}/src/golang/x/**`目录下即可。  