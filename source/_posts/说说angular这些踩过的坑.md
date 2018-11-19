title: "说说angular这些踩过的坑"
date: 2014-11-24 09:35:00
tags:
---

习惯了jquery的dom操作思想,对于angular以数据为中心，不免会有些弯路

比如在做部门select下拉级联时候，用jquery-ajax请求过来数据push归类

当第一个click时候，检测length有则append child，依次。但是，angular套路

就不一样了，在select选择时，对应的ng-model会改变值，直接数据同步了。

你不需要关系select的value怎样。数据即一切，它集成了ng-click、ng-change、

ng-show、ng-hide这些指令，我们需要在模板页绑定事件及参数。因此，在

级联的select中做ng-change事件，每次触发，把select的id传参处理函数。检测

对应的子级栏目是否存在（&amp;&amp;逻辑运算不出来，待解决），在所有子级select

中通过ng-show绑定参数，决定它是否存在，太方便了。

    对于,添加自增的select下个ng-show直接判断上个select对应model是否存在

即可