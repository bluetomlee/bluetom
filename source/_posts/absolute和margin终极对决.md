title: "absolute和margin终极对决"
date: 2014-11-12 22:29:00
tags:
---

某日,苗苗问我position和margin做动画时哪个性能好,当时我回答:

设置position:absolute时，浏览器会重新增加一篇渲染区域，

而margin在同一渲染区，所以margin性能会好些

不料网上的结论说absolute好于margin，因为margin-left这种属性不断改变时候，

这个dom节点会不断reflow,而position再另片渲染区域引起的reflow就小很多。

同事觉得依情况而定，未必absolute比margin好

我觉得蛋疼

talk is cheap,show me the code 随时决定自己试试

两个ID节点。分别嵌套了1000个节点。每个节点都是萌妹纸这才是关键

用chrome的Profiles做分析

插入500个节点的情况，

cpu内存占用 结果如下：

margin![1.png](http://www.liyi.it/usr/uploads/2014/11/2198283847.png)

position![2.png](http://www.liyi.it/usr/uploads/2014/11/454232233.png)

position运算的内存占用了10K

而margin所造成cpu用了50K

整整5倍性能显然所见

position:absolute完优margin

[demo戳我](http://codepen.io/bluetomlee/pen/Pwowmo)