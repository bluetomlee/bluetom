title: "casper爬虫用例"
date: 2016-01-13 12:23:22
tags:
---

### 模拟登陆百姓网
```javascript
  var casper = require('casper').create();
  var conf = {
      'baixing' : {
          login : 'http://www.baixing.com/oz/login',
          user  : '',
          pwd   : '',
          list  : 'http://www.baixing.com/w/posts?src=topmenu',
          fresh : [
              'http://www.baixing.com/pays/refresh/?adId=258292835',
          ]
      },
      '99cfw' : {
          login : 'http://user.99cfw.com/login/',
          user  : '',
          pwd   : '',
          fresh : [
              'http://user.99cfw.com/refresh.asp?id=zryxyzfurxswu',
              'http://user.99cfw.com/refresh.asp?id=zrztuRuvrxswu',
          ]
      }
  };

  // 99cfw
  casper.start(conf['99cfw'].login, function () {
      this.fill('form#userlogin', {
          'loginName' : conf['99cfw'].user,
          'password'  : parseInt(conf['99cfw'].pwd, 16)
      }, true);
  });

  casper.thenEvaluate(function () {
      document.querySelector('button[type="submit"]').submit();
  });

  casper.wait(500);

  casper.each(conf['99cfw'].fresh, function (self, link) {
      // var _list = document.querySelectorAll('a[href^=refresh');
      self.thenOpen(link, function () {
          this.echo(link);
      });
      // for (var i = 0; i < _list.length; i++) {
      //     _list[i].click();
      // };
  });

  casper.wait(500);

  casper.then(function () {
    this.echo('99cfw Done!');
  });

  // 百姓
  casper.thenOpen(conf['baixing'].login, function () {
      this.fill('form#authform', {
          'identity' : conf['baixing'].user,
          'password'  : parseInt(conf['baixing'].pwd, 16)
      }, true);
  });

  casper.thenEvaluate(function () {
      document.querySelector('#id_submit').click();
  });

  casper.wait(200);

  casper.thenOpen(conf['baixing'].fresh[0]);

  casper.then(function () {
    this.echo('baixing Done!')
    this.capture('step2.png');
  });

  casper.run();

```

### 自动化监控

````javascript
var casper = require('casper').create();
var fs = require('fs');
var results = [];

var conf = {
    pcResult: 'http://image.baidu.com/i?tn=baiduimage&ps=1&ct=201326592&lm=-1&cl=2&nc=1&ie=utf-8&word=%E9%B2%9C%E8%8A%B1'
};


function getTitles() {
    var titles = document.querySelectorAll('.fc-bt-right');
    return Array.prototype.map.call(titles, function (e) {
          return e.innerHTML;
    })
}

casper.start(conf['pcResult']);

casper.waitFor(function check() {
    return this.evaluate(function() {
        return document.querySelectorAll('.fc-bt-right').length > 0;
    });
}, function then() {
    results = this.evaluate(getTitles);
});

casper.run(function() {
    this.echo(results.join('\n')).exit();
    fs.write('results.txt', results.join('\n'), 'w')
});

```