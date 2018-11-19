title: "# Rmbp小记"
date: 2014-07-03 13:16:07
tags:
---

梦寐以求的mpro终于入手，解脱鼠标感觉真好，Retina显示效果太赞！

好好码代码~

系统装好后，Chorme同步,VPN翻翻，[hosts下载](http://vdisk.weibo.com/s/alR3YsOYIi7cF)

    sudo vi /etc/hosts
    `</pre>

    ## php环境配置

*   启动Apache
*   运行PHP
*   安装MySQL
*   使用phpMyAdmin
*   配置PHP的MCrypt扩展库
*   设置虚拟主机
    apache+mysql+phpmyadmin<pre>`sudo apachectl start
    //apache配置 #LoadModule php5_module libexec/apache2/libphp5.so 去除#
    sudo vi /etc/apache2/httpd.conf
    sudo cp /etc/php.ini.default /etc/php.ini
    sudo vi /etc/php.ini
    sudo apachectl restart
    // phpmyadmin
    sudo tar -xf ~/Downloads/phpMyAdmin-3.5.2.2-all-languages.tar.bz2 -C /Library/WebServer/Documents/
    sudo mv /Library/WebServer/Documents/phpMyAdmin-3.5.2.2-all-languages /Library/WebServer/Documents/phpmyadmin
    cd /Library/WebServer/Documents/phpmyadmin
    sudo cp config.sample.inc.php config.inc.php
    sudo vi config.inc.php
    //localhost改成127.0.0.1就ok了，
    //$cfg['Servers'][$i]['AllowNoPassword'] = false; 改为true，允许空密码
    