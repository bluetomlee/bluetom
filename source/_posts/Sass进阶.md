title: "Sass进阶"
date: 2014-08-05 18:51:40
tags:
---

Sass进阶

    compass create homework   //建立工程项目
    cd homework             
    compass watch
    `</pre>

    除了最初的

    <pre>`@import "../images/*.png";
    `</pre>

    ##### 通过include来调用compass生成的minin

    <pre>`@include all-images-sprites;
    `</pre>

    ##### 混合宏实现名称命名

    <pre>`@import "Color/*.png";
    .icon-qq {
        @include Color-sprite(qq);
    }
    .icon-renren{
        @include Color-sprite(renren);
    }
    .icon-163{
        @include Color-sprite(163);
    }
    `</pre>

    ##### 控制间距

    创建一个5间距的Sprite

    <pre>`//import
    $images-spacing:5px  //images为工程文件名
    @import "../images/*.png";

    //使用Sprite Maps
    $images:sprite-map("images/*.png",$spaecing:5px);
    `</pre>

    ##### 一些Sass高级用法

    <pre>`@import "icon/*.png";
    $box-padding: 5px;
    $height: icon-sprite-height(some_icon);
    $width: icon-sprite-width(some_icon);

    .somediv {
      height:$height + $box-padding;
      width:$width + $box-padding;
    }

[参考资料](http://compass-style.org/help/tutorials/spriting/)