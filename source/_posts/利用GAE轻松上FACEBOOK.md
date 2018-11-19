title: "利用GAE轻松上FACEBOOK~"
date: 2012-01-07 12:23:42
tags:
---

自从用了goagent，上facebook，twitter，看youtube那真是小菜一碟。而且看[youtube](http://www.youtube.com/)的流畅度和[优酷](http://www.youku.com/)一样,不信？你试试。
> 教程开始！！！
> 第一步：申请Google App Engine账号（其实就是申请Gmail账号，两者通用）

网址是[http://appengine.google.com](http://appengine.google.com/)

如果已有谷歌账号，那就直接登录吧。
> ![goagent](http://photo.staticsdo.com/a1/430/388/226/69589-1230840885-8.png)第二步： 创建Google App Engine的ID

顺利登录后，点击Creat an Application

![goagent](http://photo.staticsdo.com/a1/494/113/394/69577-1230840885-8.png)

接着输入你的手机号码，国家选择Other(Not Listed)

![goagent](http://photo.staticsdo.com/a1/466/372/76/69578-1230840885-8.png)

需要注意的是，手机号码前面要+86 格式如：+86 13888888888。然后等待收取手机短信，收到短信后（一串数字号码）填入表单，点send提交.

几秒后，谷歌会发来短信（免费的），里面有一串数字，填上即可。

![goagent教程](http://photo.staticsdo.com/a1/110/124/392/73870-1230840885-8.png)

点击send后，Google App Engine账号即被激活，然后就可以创建新的应用程序了。页面会自动转入“My Applications”页面，点击“Create an Application”新建应用，如下图：

[![goagent教程](http://photo.staticsdo.com/a1/46/345/509/73804-1230840885-8.jpg)](http://photo.staticsdo.com/a1/46/345/509/73804-1230840885-8.jpg)

一个Gmail账户最多可以创建十个Google App Engine应用。每个应用每天有1GB免费流量，不够的话，多申请几个就可以了(无需再进行手机验证)。下面填写新应用的必要信息，如下图：

[![goagent教程](http://photo.staticsdo.com/a1/18/143/330/73838-1230840885-8.jpg)](http://photo.staticsdo.com/a1/18/143/330/73838-1230840885-8.jpg)

在 上图中第一处添加一个应用名称，如123abc验证一下是否可用，如果通过那么123abc就是你的Appid（一定要记住这个id！），而 123abc.appspoft.com就是你的应用服务器地址了。第二个空格就是给你的应用取个名字，可以随便填，最后点击提交按钮，如果能看到下图这 个页面，就说明你成功创建了一个新的应用

![goagent教程](http://photo.staticsdo.com/a1/210/176/111/73803-1230840885-8.jpg)
> 第三步： 下载goagent客户端

下载地址：[http://code.google.com/p/goagent/](http://code.google.com/p/goagent/)

解压后会看到2个文件夹

1\. 双击server\uploader.bat(linux/mac用户请运行uploader.py),先输入你的appid然后会提示你输入Gmail 邮箱和密码，（输入密码时将看不见任何符号，但你不用管他，输完密码后按回车就可以了）接着程序会自动上传至谷歌服务器,看到方框内的文字尤其是最后一行 就表示上传成功了。

![goagent教程](http://photo.staticsdo.com/a1/210/202/120/73883-1230840885-8.png)

2.用记事本打开server文件夹下的app.yaml，在第一行的application：处输入你的id

![null](http://photo.staticsdo.com/a1/146/421/36/69584-1230840885-8.png)

3.用记事本打开load文件夹下的proxy.ini 在appid=处填上你的id

![null](http://photo.staticsdo.com/a1/210/60/157/69585-1230840885-8.png)

4.至此，所有设置都已完毕。以后每次要翻.墙前先打开load文件夹下的goagent.exe，接着在代理设置中输入ip地址127.0.0.1和端口8087，下图以谷歌的chrome为例，教你如何设置代理（点击图片可放大）

[![](http://photo.staticsdo.com/a1/46/110/475/73989-1230840885-8.jpg)](http://photo.staticsdo.com/a1/46/110/475/73989-1230840885-8.jpg)

5.有些朋友说goagent看不了youtube，其实我觉得应该与浏览器兼容性有关，还是建议大家用chrome浏览器进行观看哦。下图为证。（youtube正在正常播放哦，看进度条就知道了。）另外我的twitter地址是[http://twitter.com/MsnSun](http://twitter.com/aexwx)嘿嘿
<p>[![](http://photo.staticsdo.com/a1/18/154/238/73988-1230840885-8.jpg)](http://photo.staticsdo.com/a1/18/154/238/73988-1230840885-8.jpg)
> 总结：谷歌果然是老大，什么卫星，什么地图，什么翻墙，太造福我们了！本猫用它看[youtube](http://www.youtube.com/)，流畅的没话说。
> 
> 还有谁不懂，请留言。