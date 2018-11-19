title: "node批处理文本"
date: 2016-01-12 18:44:46
tags:
---

接到个需求，其中涉及到对txt的批处理，
node的readline也可方便处理此类文本

sample：
```
0	植物-根
1	植物-2
2	植物-3
```


代码如下：

```javascript
var line = require('readline');
var fs = require('fs');
var path = require('path');
var logFile = path.join(__dirname, 'result.txt');

var rl = line.createInterface({
	input: process.stdin,
	ouput: process.stdout,
	terminal: false
});

rl.on('line', function (line) {
	line = line
		.replace(/\d+/, '\'' + '$&' + '\':')
		.replace(/\s+/, '\'') + '\',';
	fs.appendFile(logFile, line, 'utf8', function (err) {
		if (err) throw err;
	})
})

```
