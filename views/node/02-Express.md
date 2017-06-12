# Express

## Express简介

Express 是一个简洁而灵活的 node.js Web应用框架, 提供一系列强大特性帮助你创建各种Web应用。Express 不对 node.js 已有的特性进行二次抽象，我们只是在它之上扩展了Web应用所需的功能。丰富的HTTP工具以及来自Connect框架的中间件随取随用，创建强健、友好的API变得快速又简单

## Express下载安装

https://github.com/expressjs/express

## Express示例

```
var express = require('express');
var path = require('path');
var fs = require('fs');

var app = express();

//处理静态资源
app.use(express.static(path.join(__dirname, 'statics')));

app.get('/', function(request, response) {
	fs.readFile('./views/index.html', 'utf8', function(err, data) {
		response.send(data);
	});
});

app.listen(3333, function() {
	console.log('正在监听：3333');
});
```

## Express路由

```
var express = require('express');

var router = module.exports = express.Router();

router.get('/', function(req, res) {
	res.send('index');
});

router.get('/news', function(req, res) {
	res.send('news');
});
```