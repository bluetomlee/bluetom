title: "解决Google字体长时间加载网站变白"
date: 2014-06-15 00:42:27
tags:
---

> 因为近日墙的越来越厉害,google字体也受影响
> 
> 长时间加载导致网站空白，剞劂方案两种思路

*   更换CDN加速点

        *   找到引入fonts.googleapi.com文件,一般在templets/function.php
*   include/function.php关闭google-fonts(没试)