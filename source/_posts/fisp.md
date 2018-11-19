title: "fisp上线整理"
date: 2015-7-1 22:44:00
tags:
---

>好久没发博了。整理下原来关于fisp知识。   
>曾几何时，窃以为fis | fisp是为了前端自动化部署的环境  
>Grunt、Gulp这种用node自己随便配配不是一样的效果，但是但是想错了
>smarty组合整理后台数据及前端模块片段，fis遵从commonjs以widget方式开发。也是Web Components的思想，do it

##搭建篇
###环境
node.js+php一个不能少

```
npm install -g fisp

brew install php55 -cgi
```
lights为fis包管理

```
npm install -g lights
```
初始化及安装demo

```
fisp server init
lights install pc-demo
```

###发布
>详解下fisp发布流程。  
>在项目中配置fis-conf.js，这里涉及了打包，命名空间，合并，远程发到测试机等conf。  
>当fisp release时,他会把该项目文件模块编译至*.fis-plus-tmp/*这个目录  
> 本机的环境，模拟项目调试都在此目录作为缓存。在mac中pwd为/Users/bluetom/.fis-plus-tmp,有兴趣的可以在这个目录自己玩玩

```
$ cd pc-demo
$ fisp release -r common
$ fisp release -r home
$ fisp server start
```
##Smarty模板篇


### {html *framework="frameworkPath"*}{/html} 标签

`{html}` `{/html}` 标签是 **她** 用来控制模板输出的插件，使用时替换原生 `<html>` `</html>` 标签。   
参考[输出方式(TODO)](#TODO)

### {head}{/head} 标签

`{head}` `{/head}` 标签是 **她** 用来控制模板输出的插件，使用时替换原生 `<head>` `</head>` 标签。  
参考[输出方式(TODO)](#TODO)

### {title}{/title} 标签

`{title}` `{/title}` 标签是 **她** 用来收集页面标题的插件，使用时替换原生 `<title>` `</title>` 标签。  
参考[输出方式(TODO)](#TODO)

### {body}{/body} 标签

`{body}` `{/body}` 标签是 **她** 用来控制模板输出的插件，使用时替换原生 `<body>` `</body>` 标签。  
参考[输出方式(TODO)](#TODO)
```smarty
{html her="common:static/lib.js"}
  {head}
    {title}This is title{/title}
    {require name="common:reset.css"}
    ...some thing else in head.
  {/head}
  {body}

    ...some thing outside before pagelet.

    {require name="common:page.css"}
    {pagelet id="mypagelet"}
       {require name="module:pagelet.css"}
       ...some thing inside pagelet.
    {/pagelet}

    ...some thing outside after pagelet.

  {/body}
{/html}
```

运行时输出：
```html
<!DOCTYPE html>
<html>
<head>
<title>This is title</title>
<!-- 所有pagelet之外依赖的css资源和*{html}*标签指定的框架js，会直接同步输出，其他资源都是由前端loader异步加载 -->
<link rel="stylesheet" type="text/css" href="*reset.css的真实发布路径*" />
<link rel="stylesheet" type="text/css" href="*page.css的真实发布路径*" />
...some thing else in head.
</head>
<body>
...some thing outside before pagelet.
<div id="mypagelet"></div><!-- pagelet先只输出占位div，其内容和资源在后面输出 -->
...some thing outside after pagelet.

<!-- 所有pagelet之外依赖的css资源和*{html}*标签指定的框架js，会直接同步输出，其他资源都是由前端loader异步加载 -->
<script src="*lib.js的真实发布路径*"></script>

<!-- 所有同步输出的资源，用*BigPipe.loadedResource*注册一下，告诉前端loader它们已经加载了 -->
<script>BigPipe.loadedResource(["c8ade30","3365e3d","46b833c"]);</script>

<!-- 下面会依次输出每一个pagelet的内容和资源，包括*{html}*，*{html}*是一个特殊的最顶层的pagelet -->
<!-- *{html}*资源输出begin，html包含的dom其实是同步输出到页面的，即上面的 "some thing outside pagelet." -->
<script>
BigPipe.hooks["__cb_0_1"]=function(){/*some code...*/};
BigPipe.setResourceMap({
  "c8ade30":{
     "src":"*lib.js的真实发布路径*",
     "type":"js",
     "deps":[],
     "mods":["common:static/lib.js"]
   },
  "3365e3d":{
     "src":"*reset.css的真实发布路径*",
     "type":"css",
     "deps":[],
     "mods":["common:reset.css"]
   },
   "46b833c":{...}
});
BigPipe.onPageletArrive({"id":null,"children":["mypagelet"],"deps":{"beforedisplay":["3365e3d","46b833c"],"load":[]},"hooks":{"load":["__cb_0_1"]}});
</script>
<!-- *{html}*输出end -->

<!-- *{pagelet}*内容和资源输出begin -->
<code id="__cnt_mypagelet" style="display:none"><!--
...some thing inside pagelet.
--></code>
<script>
BigPipe.setResourceMap({});
BigPipe.onPageletArrive({"id":"mypagelet","css":["依赖的 CSS 资源*pagelet.css的id*"],"js":["依赖的 JS 资源"],"container_id":"__cnt_mypagelet"});
</script>
<!-- *{pagelet}*内容和资源输出end -->

</body>
</html>
```

### {pagelet *[tag="div"]* *[bigrender]*}{/pagelet} 标签

`{pagelet}` `{/pagelet}` 标签用来标记页面中的独立区块，该区块可以被单独的加载和渲染，并且可以通过编程控制渲染时机。
生成的标签由 *`tag`* 参数指定，默认为 `"div"`。  
如果设置了bigrender属性，则会采用bigrender方式渲染。
参考[输出方式(TODO)](#TODO)

```smarty
{pagelet}
    <p>我是一个 pagelet</p>
    <p>我能被单独加载和渲染</p>
{/pagelet}
```

上面的代码在运行时会生成：

```html
<div id="自动生成的ID"></div>
<code id="另一个自动生成的ID" style="display:none"><!--
    <p>我是一个 pagelet</p>
    <p>我能被单独加载和渲染</p>
--></code>
<script>
BigPipe.onPageletArrive({"id":"DIV 的 ID","css":["依赖的 CSS 资源"],"js":["依赖的 JS 资源"],"container_id":"CODE 的 ID"});
</script>
```

会根据优化策略适时的将 html 片段插入节点中，并且保证 CSS、JS 的加载和执行顺序。

### {script *[pagelet-on="load"] [var-varName=$data]*}{/script} 标签

`{script}` `{/script}` 标签用来标注并收集页面中的代码片段。在输出时，**她** 会将收集的代码封装成函数并且自动控制调用时机。  
参考[代码执行时机(TODO)](#TODO)

`{script}` 标签支持 *`pagelet-on`* 属性，用来控制脚本执行的时机。默认为 `"load"` ，即 pagelet 的HTML加载后执行。其他可选的值和对应的执行时机如下:

 * arrive: pagelet 数据块到达时 (暂未实现)
 * beforeload: pagelet 开始加载依赖的CSS/JS资源之前 (暂未实现)
 * cssresolved: 依赖的css资源加载完成后 (暂未实现)
 * beforedisplay: 显示(innerHTML)之前
 * display: 显示之后
 * jsresolved: 依赖的js资源加载完成后 (暂未实现)
 * load: 加载完成
 * afterload: 加载完成后 (暂未实现)
 * beforeunload: 卸载之前 
 * unload: 卸载时
 * afterunload: 卸载后 (暂未实现)

为了方便代码压缩和减少转义引起的BUG，`{script}` 标签还支持类似 `var-varName=$smartyData` 参数，**她** 会自动将模板变量通过 [json_encode](http://php.net/manual/zh/function.json-encode.php) 转义并且赋值给 `varName` 变量，方便直接引用。  (暂未实现)
 **注意：`{script}`标签内不能再使用 Smarty 模板变量**

为了方便开发时语法高亮，**她** 在编译阶段引入了对 `<script runat="server"(暂定)>` 的预处理。

```html
{$name="我是含有引号( ' )的用户名"}
<script runat="server" pagelet-on="beforeload" var-userName=$name>
    var xxx = require(xxx);
    xxx.XXX();
    alert(userName);
</script>
```

上面的写法等同于：

```smarty
{$name="我是含有引号( ' )的用户名"}
{script pagelet-on="beforeload" var-userName=$name}
    var xxx = require(xxx);
    xxx.XXX();
    alert(userName);
{/script}
```

运行时代码会变为：

```html
<script>

BigPipe.hooks["系统管理的ID"] = function(require, pagelet){
    var userName = "我是含有引号( \' )的用户名";
    var xxx = require(xxx);
    xxx.XXX();
    alert(userName);
};
</script>
```

### {require *name="resourcePath"*} 标签

`{require}` 标签用来标注一个资源依赖。可以用于 CSS 和 Js 资源， *`resourcePath`* 为资源路径：

```smarty
{require name="common:js/jquery.js"}
{require name="common:css/color.css"}
```

### {define *[method="methodName"]*}{/define} 标签

`{define}` 标签用来定义一个可重用模板片段，该片段可以通过 `{widget}` 标签调用：

```smarty
{*common:widget/title/title.tpl*}

{define userName="默认用户名"}
    <!-- 一个可以重用的用户名显示组件 -->
    <dl>
        <dt>姓名</dt>
        <dd>{$userName|escape}</dd>
    </dl>
{/define}

{*调用方式如下：*}
{widget name="common:widget/title/title.tpl" userName="张三"}
```

为了方便在一个文件中定义逻辑相关的多个片段，`{define}` 和 `{widget}` 还支持 *`method`* 参数(默认为 `"__main"` )：

```smarty
{*common:widget/title/title.tpl*}

{define method="showName" userName="默认用户名"}
    <!-- 一个可以重用的用户名显示组件 -->
    <dl>
        <dt>姓名</dt>
        <dd>{$userName|escape}</dd>
    </dl>
{/define}

{*调用方式如下：*}
{widget name="common:widget/title/title.tpl" method="showName" userName="张三"}
```

### {widget *name="resourcePath" [method="methodName"]*} 标签

`{widget}` 标签用来调用用 `{define}` 定义的可重用的模板片段。  
参考[`{define}` 标签](#define-methodmethodnamedefine-%E6%A0%87%E7%AD%BE)
