title: "高性能JavaScript-笔记"
date: 2014-07-11 19:10:23
tags:
---

<p>#高性能JavaScript

1.减少全局变量访问

    //原版
    function onChange(){
        var db = document.body,
            div = document.getElementsByTagName("div")，
            i   = 0，
            len = div.length;
        while(i&lt;len){
            update(links[i++]);
        }

    }

    //优化版,访问全局变量3次可以减少至1次，N多全局变量性能将显著改善
    function onChange(){
        var doc = document,
            bd  = doc.body,
            div = doc.getElementsByTagName("div")，
            i   = 0，
            len = div.length;
        while(i&lt;len){
            update(links[i++]);
        }

    }
    `</pre>

    2.最小化重绘
    <pre>`//减少每次dom读取，1次改变
    var el = document.getElementById("lee");
    el.style.cssText='border-left:1px;border-radius:2px;';//覆盖CSS
    el.style.cssText +='border-left:1px;';//增加css
    //或者修改Class