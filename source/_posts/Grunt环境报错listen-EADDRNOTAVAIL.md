title: "Grunt环境报错listen EADDRNOTAVAIL"
date: 2014-11-18 18:49:53
tags:
---

    Running "serve" task

    Running "clean:server" (clean) task
    Cleaning .tmp...OK

    Running "wiredep:app" (wiredep) task

    Running "wiredep:sass" (wiredep) task

    Running "concurrent:server" (concurrent) task

        Running "compass:server" (compass) task
        directory .tmp/styles/ 
           create .tmp/styles/main.css (1.124s)
        Compilation took 1.129s

        Done, without errors.

        Execution Time (2014-11-18 10:32:05 UTC)
        compass:server  1.4s  ▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇▇ 100%
        Total 1.4s

    Running "autoprefixer:dist" (autoprefixer) task
    File .tmp/styles/main.css created.

    Running "connect:livereload" (connect) task
    Fatal error: listen EADDRNOTAVAIL
    `</pre>

    今下午跑了两个小时都是

    Fatal error: listen EADDRNOTAVAIL

    stackoverflow查找无果，最终嫌疑定在端口域名绑定的问题。

    解决方案如下，Gruntfile.js的connet：处修改hostname把localhost为127.0.0.1

    <pre>`    connect: {
          options: {
            port: 9000,
            // Change this to '0.0.0.0' to access the server from outside.
            hostname: '127.0.0.1',
            livereload: 35729
          },
    