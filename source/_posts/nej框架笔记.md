title: "nej框架笔记"
date: 2014-08-08 20:48:00
tags:
---

*   依赖模块

        *   `define'{pro}util.js'`
*   Nej.P命名空间

        *   私有nm前缀
*   NEJ.C
*   NEJ.X

    var _home = {a:0,b:1},
        _school = {a:"good".b:"stu",c:"class"};
        //将school属性拷贝_home
        var _obj=NEJ.X(_home,_school);
        //一个过滤器，过滤处非a值；
        var _filter = function(_vaule,_string){
            if (_string !="a")
            return false;
        }

*   基础库

        *   constant*   element /e*   event /v

                *   事件监听

                        *   `_event,'c:btn'`
            *   `_event,'a:action'`
        *   _init
        *   _allocate
        *   _destroy
        *   reset
*   ui基类
*   jst模板

        *   通过`&lt;textarea&gt;`解析
    *   jst

                *   addhtmltemplete
    *   ntp

                *   addnodetemplete