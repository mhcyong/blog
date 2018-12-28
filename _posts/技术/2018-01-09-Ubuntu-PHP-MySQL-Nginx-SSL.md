---
layout: blog
technology: true
background: green
background-image: /thumbs/ubuntu.png
date: 2018-01-09 16:19
title: Ubuntu下安装并配置PHP7+MySQL+Nginx+SSL网站环境
category: 技术
ascription: technology
tags:
- SSL
- https
- PHP
---

# 一、购买完服务器后，SSH登录进服务器，先看服务器版本信息  
`lsb_release -a`  
或者  

`apt-get install lsb-core`  

# 二、服务器基本设置  
`sudo apt-get update`

# 三、安装语言包
`sudo apt-get install -y language-pack-en-base`

# 四、设置语言
`sudo locale-gen en_US.UTF-8`

# 五、安装常用的工具vim,htop,git等
`sudo apt-get install -y vim htop git`

# 六、开始安装PHP，首先更新PPA
```
sudo apt-get install software-properties-common
sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
sudo apt-get update
apt-cache search php7.1（查看刚才是否成功更新了PHP）
sudo apt-get -y install php7.1 （安装PHP7.1）
php -v（查看版本）
sudo apt-get -y install php7.1-mysql （安装数据库模块）
sudo apt-get install php7.1-fpm
sudo apt-get install php7.1-curl php7.1-xml php7.1-mcrypt php7.1-json php7.1-gd php7.1-mbstring （安装其它模块）
```

# 七、安装MYSQL
`sudo apt-get -y install mysql-server-5.7`  

使用命令行在ubuntu下安装mysql可视化工具MySQL-workbench  

方案一：如果你已经装好mysql的相关服务，那么直接使用如下命令即可安装：  

`sudo apt-get install mysql-workbench`  

方案二：如果你还未装好mysql的相关服务，那么你可以参考：Ubuntu安装MySQL-workbench  

http://blog.csdn.net/jgirl_333/article/details/48575281  

# 八、安装nginx

在你已经安装了Apache2的话，那么使用这些命令先删除再安装nginx：  
```
service apache2 stop
sudo update-rc.d -f apache2 remove
sudo apt-get remove apache2

sudo apt-add-repository ppa:nginx/stable
sudo apt-get update

sudo apt-get -y install nginx
```

# 九、配置PHP
```
sudo vim /etc/php/7.1/fpm/php.ini
// 将cgi.fix_pathinfo=1这一行去掉注释，将1改为0
按/进入搜索  :wq退出
sudo vim /etc/php/7.1/fpm/pool.d/www.conf
// 配置这个 listen = /var/run/php7.1-fpm.sock
```

# 十、配置Nginx
在nginx目录下，sites-available/default里面  
sudo vim /etc/nginx/sites-available/default  
修改nginx配置  
```
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        root /var/www/laravel-ubuntu/public;
        index index.php index.html index.htm;

        # Make site accessible from http://localhost/
        server_name localhost;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ /index.php?$query_string;
                # Uncomment to enable naxsi on this location
                # include /etc/nginx/naxsi.rules
        }
        location ~ \.php$ {
                try_files $uri /index.php =404;
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                fastcgi_pass unix:/var/run/php7.1-fpm.sock;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
        }
```
`sudo service nginx restart（重启nginx）`

# 十一、创建网站目录
```
cd /var/www
mkdir /var/www （如果没有此目录，创建。）
sudo chown -R www-data:www-data  /var/www    （权限给www用户组）
sudo chmod -R 775 storage/
sudo service php7.1-fpm restart
```