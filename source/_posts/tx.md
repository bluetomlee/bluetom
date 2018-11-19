title: "腾讯面试整理"
date: 2015-1-1 22:44:00
tags:
---


###一、

> 盒模型

w3c不含padding、border

IE模型包含padding、border


> 图片加载不到，重绘怎么解决

初始化,||既定图片默认值


> 瀑布流实现

固定行宽，所有比例缩放至行宽



--------------------
###二、
####FE:

1.ajax回调容错处理

2.瀑布流实现

3.多种模板怎么实现

4.Window.requestAnimationFrame

5.图片缩放实现方式

6.事件模型
	
	原始事件模型
	W3C事件模型，捕获，事件处理，冒泡
	IE事件模型
		冒泡、处理（没有捕获）

7.IE的冒泡详解，阻止方法，preventDefault哪些常用到
	
	submit阻止默认行为
	阻止冒泡：
		ie:window.event.cancelbabel()
		w3c:e.stoppropagation()
	阻止默认行为：
		ie:e.returnValue = false;
		w3c:e.preventDefault();	

9.domready，onload区别

	domready🌲绘制完毕
	window.onload表示文档中外部资源全部加载完毕
	
10.跨域处理

	1.document.domain+ifame(主域相同而子域不同)
	2.jsonp服务器返回script
	3.html5原生api中PostMessage(string,url)
		window.addEventListener('message')
	4.flash

11.前端优化方案

12.a标签阻止行为几种方式


####网络、

1.域名解析过程

2.三次握手

3.TCP/IP协议详解

4.UDP/TCP区别

5.线程和进程区别

6.整个网站访问过程

7.http状态码

8.图片本地缓存处理

9.USI七层模型原理


