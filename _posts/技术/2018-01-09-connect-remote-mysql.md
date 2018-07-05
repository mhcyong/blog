---
layout: blog
technology: true
background: red
background-image: https://obdr74yw6.qnssl.com/mysql.jpg
date: 2018-01-09 15:54
title: 远程连接服务器的MySQL数据库
category: 技术
cslug: technology
tags:
- mysql
- 数据库
---

有的时候，我们需要在本地利用客户端连接服务器上的数据库去查看了解情况，因为这样非常的直观，而事实上，也有比较好的客户端，比如Navicat，workbench方便操作。  
这里推荐Navicat远程操作。  
```
mysql -u root -p
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '密码' WITH GRANT OPTION;
```
修改`etc/mysql/my.cnf`,在mysql5.7以上，文件地址和名称发生了变化，在`/etc/mysql/mysql.conf.d/mysqld.cnf`下。  
将 `bind-address = 127.0.0.1` 这一行注释掉, 即修改为:`#bind-address = 127.0.0.1`  
这样就可以通过Navicat等客户端远程连接操作数据库了。