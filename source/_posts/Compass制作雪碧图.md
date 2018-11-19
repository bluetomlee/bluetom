title: "Compass制作雪碧图"
date: 2014-07-28 21:07:00
tags:
---

雪碧图笔记

1.Pscc开启生成->图像资源

图层或图层组命名规则：

hi-res/leftbar-rec-prs@2x.png24 +50% leftbar-rec-prs.png24  //生成原大小和50%长款的两张图

参考官网

2.Node.js配置

官网下载Node.js->下载Ruby->修改win7环境变量->修改gem源->安装Compass

3.Compass雪碧图制作
<pre>
`
//Compass环境搭建
compass create ipad
compass watch
mkdir images
//style.css
@import "leftbar/*.png";@include all-leftbar-sprites;
`
</pre><p>[参考资料](http://www.w3cplus.com/preprocessor/compass-image-sprite.html)