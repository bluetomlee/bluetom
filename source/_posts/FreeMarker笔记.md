title: "FreeMarker笔记"
date: 2014-09-19 11:11:00
tags:
---

##### 开发常用标签:

*   ${...}：为取值
*   &lt;#...>：FTL标签
*   &lt;@>：自定义宏
*   &lt;#-- Comments 注释-->

##### if指令

    &lt;#if user == "bluetom"&gt;...&lt;/#if&gt;
    &lt;#if user[0].age&lt;user[1].age&gt;
        hello,world
    &lt;#else&gt;
    &lt;/#if&gt;
    `</pre>

    ##### list指令

    <pre>`&lt;#list userlist as item&gt;
    ...
    &lt;/#list&gt;
    `</pre>

    两个特殊的循环变量：

    item_index: 当前变量的索引值。

    item_has_next: 是否存在下一个对象。

    &lt;#break/>指令离开loop循环

    ##### switch

    <pre>`&lt;#switch value&gt;
    &lt;#case refValue1&gt;
    ...
    &lt;#break&gt;
    &lt;#case refValue2&gt;
    ...
    &lt;#break&gt;
    ...
    &lt;#case refValueN&gt;
    ...
    &lt;#break&gt;
    &lt;#default&gt;
    ...
    &lt;/#switch&gt;
    `</pre>

    #### include指令

    <pre>`&lt;#include "*/commons/footer.ftl"&gt;
    `</pre>

    #### escape指令

    <pre>`//解析模板用
    &lt;#escape x as x?html&gt;
    Customer Name:${customerName}
    Items to ship;
    &lt;#escape x as itemCodeToNameMap[x]&gt;
       ${itemCode1}
       ${itemCode2}
       ${itemCode3}
       ${itemCode4}
    &lt;/#escape&gt;
    &lt;/#escape&gt;
    `</pre>

    #### assign指令

    为模板页面创建、替换一个顶层变量

    <pre>`&lt;#assign x&gt;
    &lt;#list ["星期一", "星期二", "星期三", "星期四", "星期五", "星期六"] as n&gt;
    ${n}
    &lt;/#list&gt;
    &lt;/#assign&gt;
    `</pre>

    #### macro , nested , return指令

    macro可以用于实现自定义指令,通过使用自定义指令,可以将一段模板片段定义成一个用户指令,使用macro指令的语法格式如下:

    <pre>`&lt;#macro name param1 param2 ... paramN&gt;
    ...
    &lt;#nested loopvar1, loopvar2, ..., loopvarN&gt;
    ...
    &lt;#return&gt;
    ...
    &lt;/#macro&gt;

在上面的格式片段中,包含了如下几个部分:

name:name属性指定的是该自定义指令的名字,使用自定义指令时可以传入多个参数

paramX:该属性就是指定使用自定义指令时报参数,使用该自定义指令时,必须为这些参数传入值

nested指令:nested标签输出使用自定义指令时的中间部分

nested指令中的循环变量:这此循环变量将由macro定义部分指定,传给使用标签的模板

return指令:该指令可用于随时结束该自定义指令