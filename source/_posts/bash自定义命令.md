title: "bash自定义命令"
date: 2015-03-09 13:46:00
tags:
---

alias fispr='fisp server restart'

想自定义命令，发现重启会失效

解决办法：

    cd
    $ vi .bash_aliases
    `</pre>

    将下列常用快捷命令copy

    <pre>`source ~/.bash_aliases
    `</pre>

    附上常用命令

    <pre>`alias nginx.start='sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.nginx.plist'
    alias nginx.stop='sudo launchctl unload /Library/LaunchDaemons/homebrew.mxcl.nginx.plist'
    alias nginx.restart='nginx.stop &amp;&amp; nginx.start'
    alias php-fpm.start="launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php55.plist"
    alias php-fpm.stop="launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.php55.plist"
    alias php-fpm.restart='php-fpm.stop &amp;&amp; php-fpm.start'
    alias mysql.start="launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist"
    alias mysql.stop="launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist"
    alias mysql.restart='mysql.stop &amp;&amp; mysql.start'
    alias nginx.logs.error='tail -250f /usr/local/etc/nginx/logs/error.log'
    alias nginx.logs.access='tail -250f /usr/local/etc/nginx/logs/access.log'
    alias nginx.logs.default.access='tail -250f /usr/local/etc/nginx/logs/default.access.log'
    alias nginx.logs.default-ssl.access='tail -250f /usr/local/etc/nginx/logs/default-ssl.access.log'
    alias nginx.logs.phpmyadmin.error='tail -250f /usr/local/etc/nginx/logs/phpmyadmin.error.log'
    alias nginx.logs.phpmyadmin.access='tail -250f /usr/local/etc/nginx/logs/phpmyadmin.access.log'
    alias fispr='fisp server restart'
    alias fispo='fisp server open'
    