title: "CSS优先级"
date: 2014-10-11 12:38:00
tags:
---

看到寒冬的面试题

考察优先级问题，反正会出很多莫名其妙的变形，比如将style标签写在body后与body前有什么区别，比如同一dom应用多个class其应该如何表现，比如class a定义颜色为blue，class b定义颜色为red，同时应用到dom上，dom作何显示。。。

整理资料如下

    Css代码  
    #navigator {  
        height: 100%;  
        width: 200;  
        position: absolute;  
        left: 0;  
        border: solid 2 #EEE;  
    }  

    .current_block {  
        border: solid 2 #AE0;  
    }  
    `</pre>

    查找一些教材中（w3schools等），只说css的顺序是“元素上的style” > “文件头上的style元素” >“外部样式文件”，但对于样式文件中的多个相同样式的优先级怎样排列，没有详细说明。经过测试和继续搜索，得知优先级如下排列：

1.  样式表的元素选择器选择越精确，则其中的样式优先级越高：
    id选择器指定的样式 > 类选择器指定的样式 > 元素类型选择器指定的样式
    所以上例中，#navigator的样式优先级大于.current_block的优先级，及时.current_block是最新添加的，也不起作用。
2.  对于相同类型选择器制定的样式，在样式表文件中，越靠后的优先级越高
    注意，这里是样式表文件中越靠后的优先级越高，而不是在元素class出现的顺序。比如.class2 在样式表中出现在.class1之后：

    <pre>`Css代码  
    .class1 {  
        color: black;  
    }  

    .class2 {  
        color: red;  
    }  
    `</pre>

    而某个元素指定class时采用 class="class2 class1"这种方式指定，此时虽然class1在元素中指定时排在class2的后面，但因为在样式表文件中class1处于class2前面，此时仍然是class2的优先级更高，color的属性为red，而非black。

1.  如果要让某个样式的优先级变高，可以使用!important来指定：

    <pre>`Css代码  
    .class1 {  
        color: black !important;  
    }  

    .class2 {  
        color: red;  
    }  
    `</pre>

    此时class将使用black，而非red。

    对于一开始遇到的问题，有两种解决方案：

1.  将border从#navigator中拿出来，放到一个class .block中，而.block放到.current_block之前：

    <pre>`Css代码  
    #navigator {  
        height: 100%;  
        width: 200;  
        position: absolute;  
        left: 0;  
    }  

    .block {  
        border: solid 2 #EEE;  
    }  

    .current_block {  
        border: solid 2 #AE0;  
    }  
    `</pre>

    需要莫仁为#navigator元素指定class="block"

1.  使用!important:

    <pre>`Css代码  
    #navigator {  
        height: 100%;  
        width: 200;  
        position: absolute;  
        left: 0;  
        border: solid 2 #EEE;  
    }  

    .current_block {  
        border: solid 2 #AE0 !important;  
    }  

此时无需作任何其他改动即可生效。可见第二种方案更简单一些。