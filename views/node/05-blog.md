# 小项目

## 搭建项目结构

## 安装第三方包

express、xtpl、mongodb

## 设置静态资源

app.use('/statics', express.static(path.join(__dirname, 'statics')));

## 设置xtpl模板

//app.js 中设置模板
app.set('views','./views');
app.set('view engine', 'html');
app.engine('html', xtpl.renderFile);

//控制器中输出首页
controller.index = (req, res) => {
	res.render('index', {});
} 

## 获取数据，渲染首页

## 详细页面

## 无刷新评论功能

## 自己解析post的数据

let data = '';
req.on('data', (chunk) => {
	data += chunk;
})

req.on('end', () => {
	let json = parse(data);
})

function parse(data) {
	if(!data) {
		return;
	}
	var json = {};
	let array = data.split('&');
	array.forEach(function(item, index) {
		var data = item.split('=');
		if(data && data.length >= 2) {
			json[data[0]] = data[1];
		}
	})
	return json;
}

## 使用第三方包解析post数据 body-parser

- 官网
https://github.com/expressjs/body-parser

- 安装
npm install body-parser --save

- 使用
var bodyParser = require('body-parser')
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())

req.body 就是post过来的数据

## 获取客户端ip地址

req.socket.remoteAddress


## 后台管理--接口

## layer插件

http://layer.layui.com/

## 登录

## Cookie

- 在客户端保存数据的一种方式  
    * 保存少量数据4k左右，客户端和服务器都可以读写cookie
    * 如果只是存储数据，可以使用localStorage替换，可以存储5M
    * 不可以跨域
- 服务端写Cookie
    * 存储在内存
    
    ```javascript
    res.setHeader("Set-Cookie","name=zhangsan1");
    ```

    * 存储在文件
    
    ```javascript
    res.setHeader("Set-Cookie","name=zhangsan1; path=/; domain=.tt.com; max-age=180");
    ```
    
    * 参数
        - path  设置路径，哪个路径可以访问cookie
        - expires 设置过期时间，是日期，服务器的日期可能和客户端的日期不一样
        - max-age 设置过期时间，秒，第一次访问的时间开始
        - domain  设置可以跨子域访问cookie

- 封装读取cookie
    
```javascript
let cookie = module.exports;
cookie.getCookie = (req,key)=>{
    var Cookies = {};
    req.headers.cookie && req.headers.cookie.split(';').forEach(function( Cookie ) {
        var parts = Cookie.split('=');
        Cookies[ parts[ 0 ].trim() ] = ( parts[ 1 ] || '' ).trim();
    });
    return Cookies[key];
}
```

## Session

- 保持会话状态
- 服务端+客户端实现
- 模拟Session的实现

```javascript
const express = require("express");

const cookie = require("../tools/cookie");

let demo = module.exports = express.Router();
demo.prefix = "/session";
let session = {sids:[]};
//{sids:["1111","222"], "1111": {name:zhangsan},}
demo.get("/get", (req, res) => {
    res.send(req.headers.cookie);
});
demo.get("/login/:name",(req, res) => {
    let sid =cookie.getCookie(req, "sid");
    //第一次登录，判断是否有sid，如果没有sid生成一个，并跳转会当前页面
    if(!sid) {
        //唯一标示一个客户端
        sid = Math.random();
        //模拟登录
        res.setHeader("Set-Cookie","sid="+ sid + "; path=/session");

        session.sids.push(sid);

        res.redirect(req.originalUrl);
        
        //console.log(req.originalUrl);
    }else{

        //模拟登录
        res.setHeader("Set-Cookie","name="+req.params.name+"; path=/session");

        session[sid] = {name: req.params.name};

        res.send("<a href='/session'>到首页</a>");

    }

});

demo.get("/",(req, res) => {

    //req.headers.cookie

    //判断是否登录成功，先获取sid，根据sid获取当前的登录信息
    let sid =cookie.getCookie(req, "sid");

    //根据sid获取 登录信息
    let obj = session[sid];

    //模拟权限的判断
    if(obj && obj.name) {
        res.send("后台首页")
    }else{
        res.send("请先登录");
    }
});
```

## 使用express-session简化session开发

- 官网

https://github.com/expressjs/session

- 下载

npm install express-session --save

- 使用
var session = require('express-session');
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: false
}))




- 说明
	+ secret：用来对session数据进行加密的字符串.这个属性值为必须指定的属性。
	+ name：表示cookie的name，默认cookie的name是：connect.sid。
	+ maxAge：cookie过期时间，毫秒。
	+ resave：是指每次请求都重新设置session cookie，假设你的cookie是6000毫秒过期，每次请求都会再设置6000毫秒。
	+ saveUninitialized： 是指无论有没有session cookie，每次请求都设置个session cookie ，默认给个标示为 connect.sid。
    


## 处理错误

//处理404的错误
app.use((req, res) => {
    res.status(404);
    res.redirect("/www/web/404.html");
})

//处理500的错误
app.use((err, req, res, next) => {
    //err 记录到日志文件
    res.status(500);
    res.redirect("/www/web/500.html");
})