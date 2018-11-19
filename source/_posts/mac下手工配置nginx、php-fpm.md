title: "mac下手工配置nginx、php-fpm"
date: 2014-12-02 15:43:00
tags:
---

mac自带的php版本略老，

apache太吃内存，跑起百来M，nginx 10+M就够了

索性把之前的全删了

brew install nginx

brew tap josegonzalez/homebrew-php

brew install mysql

brew install phpmyadmin

cd /usr/local/etc/nginx/

sublim nginx.conf

        server {
            listen       80;
            server_name  localhost;

            #charset koi8-r;

            #access_log  logs/host.access.log  main;

            location / {
                root   /usr/local/var/www;
                index  index.html index.htm index.php;
           }
            location ~ \.php$ {
                fastcgi_pass   unix:/usr/local/var/run/php-fpm.socket;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                include        fastcgi_params;
            }

php改为socket连接

配置好phpmyadmin

create new Server

3306配置就搞定