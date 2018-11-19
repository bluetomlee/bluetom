title: "html-tag-filter"
date: 2014-11-07 16:28:00
tags:
---

后台传过来的html，需要过滤style类似多余属性

如果操作dom用jquery很方便的removeAttr()即可

纯文本还是需要正则的，手写个过滤器

需要说明的是,正则增加js变量写法就不一样了

两种方式

1.通过构造函数new RegExp()字符串和变量拼接实现

2.通过eval解析并执行,但是极不推荐,性能和安全是问题.

js如下

    (function(){
        var doc= document;
            a = doc.getElementById('before'),
            b = doc.getElementById('after'),
            c = doc.getElementById('submit'),
            t = doc.getElementById('tag');
        c.onclick = function(){
            filter(a.value,t.value);
        }
        function filter(v,tag){
            var result,regular;
            regular = new RegExp(" " + tag + "=" + "((\"([^\"]+)\")|(\'([^\']+)\'))","gim");
            result = v.replace(regular,'');
            b.value = result;
        }

    })()

[戳我](http://codepen.io/bluetomlee/pen/ygHdb)