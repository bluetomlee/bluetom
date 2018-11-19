title: "Error: EACCES, permission denied 解决"
date: 2014-12-02 15:26:00
tags:
---

配置yeomanu环境,denied总报错

     Would you like to include Bootstrap? Yes
    ? Would you like to use the Sass version of Bootstrap? Yes
    ? Which modules would you like to include? angular-animate.js, angular-cookies.js, angular-resource.js, angular-route.js, angular-sanitize.js
    identical app/styles/main.scss
    identical app/index.html
       create bower.json

    fs.js:438
      return binding.open(pathModule._makeLong(path), stringToFlags(flags), mode);
                     ^
    Error: EACCES, permission denied 'bower.json'
        at Object.fs.openSync (fs.js:438:18)
        at Object.fs.writeFileSync (fs.js:977:15)
        at Generator.&lt;anonymous&gt; (/usr/local/lib/node_modules/generator-angular/node_modules/yeoman-generator/lib/actions/actions.js:217:10)
        at processImmediate [as _immediateCallback] (timers.js:345:15)

    `</pre>

    之前以为是node模块权限不够，所以chmod node_module，尝试未果

    窃以为是网站目录的权限问题了，一行搞定

    <pre>`sudo chown yourusername:admin /yourdocument
    