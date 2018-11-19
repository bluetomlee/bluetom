title: hexo升级https
date: 2016-01-14 11:31:55
tags:
---

### ssl申请

- 申请免费的SSL，注册clouldflare服务商的服务.	   
- 登陆后将nameserver设置成clouldflare提供的地址    

### ssl设置
- cname转向bluetomlee.github.io	   
- 后台顶部的Crypto中，进入Crypto，将SSL选项设置为“Flexible”，这个的意思是访客到cf的过程是加密的，而cf到github pages不是加密的
- 将hexo根目录配置文件_config.yml，	
	添加`url: https://liyi.it` 与
	`enforce_ssl: https://liyi.it`

### 解决多说评论https
多说大部分资源已经支持了https协议，但是头像地址仍是http，所以会导致地址栏变灰色，不能直视。	

解决方案如下:	
将多说`embed.js`下载至hexo本地，	
然后将`https://liyi.it/js/embed.js`本地页面引入，
找到560行	
```javascript
  avatarUrl: function(e) {
     return e.avatar_url || rt.data.default_avatar_url
  },
```

修改如下代码
```javascript
   avatarUrl: function(e) {
     if(location.protocol === 'https:') {
         return 'https://liyi.it/img/avatar.jpeg';
     }
     return e.avatar_url || rt.data.default_avatar_url
   },
```
首页、文章页均为绿色。不过表情的静态资源仍是http。 

解决方案两种：		 
1.替换为本地表情		
2.直接用disqus，支持https协议

done，效果如下	
![](/img/https.png)