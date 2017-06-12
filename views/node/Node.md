# Node

## 课程安排

Node介绍
Express
模块
ES6语法
mogodbDB
博客项目

## Node介绍

官网
https://nodejs.org

```
Node.js 是一种建立在Google Chrome's V8 引擎上的non-blocking(非阻塞),event-driven(基于事件的)I/O平台。Node.js平台使用的开发语言是JavaScript，平台提供了操作系统底层的API，方便做服务器端编程，
具体包括：文件操作、进程操作、通信操作等系统模块，支持模块化的开发
```

C/S

- 服务端server
- 客户端client

B/S
browser 浏览器
server  服务器



## Node 可以做什么

- 高性能的网站服务器
- 简单易用的命名行应用程序


- gulp、less
- i5ting
  https://github.com/i5ting/tocmd.npm
- browser-sync
  http://www.browsersync.cn/


- 实时多人游戏后台服务器
- 高大上的桌面应用程序
  electron


- 使用 Web 技术 作为解决方案


- 底层的物联网开发
- 移动开发


- 使用 Web 技术作为解决方案

## 安装Node.js

查看Node是否安装成功/查看Node的当前版本

```
node -v
```

## 切换源

- 手工切换
  国内
  https://registry.npm.taobao.org
  国外
  http://registry.npmjs.org/

  切换
  npm config set registry https://registry.npm.taobao.org
  配置后可通过下面方式来验证是否成功
  npm config get registry

- 使用cnpm
  安装：npm install -g cnpm --registry=https://registry.npm.taobao.org

## 学习Node.js的网站

- 官网
  https://nodejs.org
  https://github.com/nodejs/node
- Node.js中文社区
  https://cnodejs.org/
- 书籍
  深入浅出Node.js

## Hello World

- 新建一个js文件
- 书写js代码
- 启动命令提示符
- 切换到js所在的目录，使用node运行js：    node   xxx.js

## 环境变量

当要求系统运行一个程序而没有告诉它程序所在的完整路径时，
系统首先在当前目录下面寻找该程序，
如果找不到，则系统会跑到path中指定的路径去找，如果找到，直接运行，
如果path环境变量中也没有找到，则直接提示不是内部或外部命令，也不是可运行的程序

当设置完环境变量之后要重启cmd

添加 path 环境变量的两种方式：

一：直接在path环境变量中加入程序所属目录的绝对路径，

```
两边以 **英文分号** 进行分隔。
```

例如 `feiq.exe` 程序的绝对路径是 `C:\Program Files\feiQ`，
则在 `path` 中添加 `;C:\Program Files\feiQ;`

二：也可以在外部先定义一个变量名，值就是程序所属目录的绝对路径，

```
然后在 path 中以 `%变量名%` 的方式引入，两边以分号分隔
```

例如 `qq.exe` 程序的绝对路径是 `C:\Program Files (x86)\Tencent\QQ\Bin`，
则先定义一个变量名 `QQ_HOME` ，变量值就是 `C:\Program Files (x86)\Tencent\QQ\Bin`，
然后在 `path` 中填入变量名：`;%QQ_HOME%;`

## Node.js快速体验

- 读写文件

var fs = require('fs');
fs.readFile();
fs.writeFile();

- 处理http请求

var http = require('http');

## path模块

可以处理字符串路径问题，拼接两个路径
var path = require('path');
path.join('c:/abc', 'xyz');

## http模块演示

- 根据不同请求，返回不同响应内容
- 返回html
- 读取文件的路径问题


- 相对路径，相对于当前编写的文件查找文件
  fs.readFile('./statics/css/style.css',....); 
- 根路径，在当前文件所处的跟目录查找文件，c:/statics/css.....
  fs.readFile('/statics/css/style.css',....); 

## Content-Type(MIME类型)

http://www.w3school.com.cn/media/media_mimeref.asp

## xtpl 模板引擎

- 官网

https://github.com/xtemplate/xtpl

- 安装

npm install xtpl xtemplate --save



## 结合静态页面的案例

准备网站的icon
准备静态页面

## 相关工具

使用到的Node.js的模块

- path
  path.join(__dirname, 'data/a.txt')  拼接目录

- url
  url.parse(s, true).query    解析url上的参数

- 当前文件路径

  __filename 执行的当前的文件的路径
  __dirname  执行的当前的文件所在的目录


- MIME模块

https://github.com/broofa/node-mime

在当前项目使用npm安装第三方包
1、在当前项目文件夹 打开命令窗口  输入  npm init /  npm init -y   创建了package.json
2、安装包   npm install 包名  --save(在package.json中记录依赖)

## 模板引擎 xtpl

## 封装render方法



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

# Node.js中的模块化

## Node.js的api文档

https://nodejs.org/dist/latest-v6.x/docs/api/

## 什么是模块化

模块化是指解决一个复杂问题时自顶向下逐层把系统划分成若干模块的过程，有多种属性，分别反映其内部特性。

## 模块化要解决的问题

1. 命名冲突
2. 文件依赖 

## Node.js中的模块化

```
在后台开发语言中，比如Java、C#。他们都是隐含模块化的，Node.js默认帮我们提供了模块化这种机制。
  在服务器端，我们想要使用底层的一些功能需要导入一些“包”来对其操作，比如操作文件、网络需要导入对应的包。其它语言中都是基于类来实现的模块化的思想，使用类来组织文件和文件之间的关联。
  而Node.js中使用的是JavaScript语言，ECMAScript仅仅规定了基本的语法的书写，并没有规定文件之间
关联，也就是说每个js文件之间是独立的，Node.js已经帮我们实现了js文件之间的关联（模块化）
  Node.js中的模块化是基于CommonJS规范的
```

## Node.js中的模块化分类

1. 核心模块(系统提供的模块)
2. 文件模块(自定义模块)
3. 第三方模块

## 核心模块

- path模块
- url模块
- http模块
  ……

## 核心模块的存储位置

- 核心模块存储在node.exe中，当node.exe运行的时候，核心模块会被加载，require的时候会加载到内存
- 在github上可以找到源代码，lib文件夹下
- 核心模块的执行速度比较快

## 文件模块

- 定义文件模块

```
function add(a,b) {
      return a + b;
  }
  //导出成员
  exports.add = add;
  //module.exports.add = add;
```

- 使用文件模块

```
 var obj = require("./add.js");
  console.log(obj.add(5,6));
```

- 注意：

文件模块的使用和核心模块不同

```
 //使用相对于main.js 的方式查找add.js
  var obj = require("./add.js");
  var obj = require("./add");
  //下面这种方式是引用核心模块或者包
  //var obj = require("add");
```

## 模块的加载顺序

- 优先从缓存加载模块或者包
- 加载文件模块要使用相对路径 ./ ../
- 文件模块的加载可以不写后缀名，如果不写后缀名按照 .js > .node > .json的顺序加载
- 加载json文件，推荐写上后缀.json
- 加载核心模块或包，不写路径和后缀
- module.paths 加载node_modules的时候，按此数组的顺序加载

## module.exports 和 exports的区别

- 当模块被加载后会自动创建一个空对象，module.exports指向这个空对象，最后导出的也是这个对象
- exports是module.exports的引用
- exports只能导出成员，不能直接赋值
- exports既可以导出成员，也可以导出对象

## 使用模块完成案例

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

```
res.render('index', {});
```

} 

## 获取数据，渲染首页

## 详细页面

## 无刷新评论功能

## 自己解析post的数据

let data = '';
req.on('data', (chunk) => {

```
data += chunk;
```

})

req.on('end', () => {

```
let json = parse(data);
```

})

function parse(data) {

```
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
```

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

  - 保存少量数据4k左右，客户端和服务器都可以读写cookie
  - 如果只是存储数据，可以使用localStorage替换，可以存储5M
  - 不可以跨域

- 服务端写Cookie

  - 存储在内存

  ```javascript
  res.setHeader("Set-Cookie","name=zhangsan1");
  ```

  - 存储在文件

  ```javascript
  res.setHeader("Set-Cookie","name=zhangsan1; path=/; domain=.tt.com; max-age=180");
  ```

  - 参数
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
  - secret：用来对session数据进行加密的字符串.这个属性值为必须指定的属性。
  - name：表示cookie的name，默认cookie的name是：connect.sid。
  - maxAge：cookie过期时间，毫秒。
  - resave：是指每次请求都重新设置session cookie，假设你的cookie是6000毫秒过期，每次请求都会再设置6000毫秒。
  - saveUninitialized： 是指无论有没有session cookie，每次请求都设置个session cookie ，默认给个标示为 connect.sid。

## 处理错误

//处理404的错误
app.use((req, res) => {

```
res.status(404);
res.redirect("/www/web/404.html");
```

})

//处理500的错误
app.use((err, req, res, next) => {

```
//err 记录到日志文件
res.status(500);
res.redirect("/www/web/500.html");
```

})



# MongoDB

## 什么是MongoDB

MongoDB一个基于分布式文件存储的开源数据库系统。
MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

## 什么是数据库

存储数据的仓库

## 相关概念

数据库(database)->集合(collection)->文档(document)->域(field)

## 安装

## 学习手册

http://www.runoob.com/mongodb/mongodb-tutorial.html

## MongoDB基本使用

- 启动MongoDB

mongod --dbpath 指定存放数据库的路径

- 连接到MongoDB的示例

mongo

- 查看数据库

  show dbs  	查看所有数据库
  db 	  		查看当前数据库
  use 数据库名称切换数据库(如果数据库不存在会自动创建)
  db.dropDatabase()   删除数据

- 增删改查命令


- 插入文档
  db.集合名称.insert(document);

示例：
db.students.insert({name: "张三", age: 18})

- 更新文档

db.集合名称.update(
   提交,
   更新内容,
   可选参数
)

示例：
db.students. ({name: "张三"}, {age: 20});

//如果没有找到对应的值，则插入
//如果有多个匹配的结果，只会修改第一个结果
db.students.update({name: "张三"}, {age: 20}, {

```
upsert: true
```

});

//$set 修饰要更新的域，如果不存在则创建
db.students.update({name: "张三"}, {$set: {age: 20}}, {

```
upsert: true
```

});

//修改所有匹配的结果
db.students.update({name: "张三"}, {$set: {age: 20}}, {

```
multi: true
```

});

- 删除文档

db.集合名称.remove(
   条件,
   justOne(是否只删除一个文档)
)

//只删除一个满足条件的文档
 db.students.remove({name:18})
 //删除所有满足条件的文档
 db.students.remove({name:18}, true)

- 查询文档

db.students.find()
db.students.find().pretty()



- save方法

db.集合名称.save(document)
不指定_id，类似insert
指定_id，类似update
db.studetns.save({

```
"_id" : ObjectId("56064f89ade2f21f36b03136"),
………………
```

})

## Node.js中操作MongoDB

- 安装插件

https://github.com/mongodb/node-mongodb-native

npm install mongodb --save

- 连接到MongoDB服务器

1. 创建MongoDB的客户端
   var mongodb = require('MongoDB');
   var mongoClient = mongodb.MongoClient;

2. 连接字符串
   var url = 'mongodb://localhost:27017/itcast';

3. 连接到服务器
   mongoClient.connect(url, function(err, db) {
   if(err) {

   ```
   throw err;
   ```

   }
   //进行数据库操作

   //关闭数据库
   db.close();
   });

- 插入数据


- 插入数据

//获取集合
var students = db.collection('students');
//插入一条数据
students.insertOne({name: '刘备', age: 18}, function(err, result) {

```
if(err) {
	throw err;
}
console.log(result);
```

});

//插入多条数据
students.insertMany([

```
{name: '李四', age: 19},
{name: '王五', age: 20}
```

], function (err, result) {

```
if(err) {
	throw err;
}
console.log(result);
```

})

- 更新数据

//更新一条数据
students.updateOne({name: '刘备'}, {$set: {age: 20}}, function(err, result) {

```
if(err) {
	throw err;
}
console.log(resu);
```

})

//更新多条数据
students.updateMany({name:'abc'}, {$set: {age: 111}}, {multi: true}, function(err, result) {

```
if(err) {
	throw err;
}
console.log(result);
```

})

- 删除数据

students.deleteOne({name:'abc'},  function(err, result) {

```
if(err) {
	throw err;
}
console.log(result);
```

})

students.deleteMany({name:'abc'},  function(err, result) {

```
if(err) {
	throw err;
}
console.log(result);
```

})

- 查询数据

students.find({name:'李四'}).toArray(function(err, result) {

```
console.log(result);
```

})

students.find().toArray(function(err, result) {

```
console.log(result);
```

})



- 根据id查询一条数据

var ObjectID = require('mongodb').ObjectID;
posts.findOne({_id: ObjectID('58abf1bfc692de395ccdd2b0')}, function(err, data) {

```
console.log(data);
```

});

# ECMAScript6语法

- 为什么要学习ES6
    * ES6也叫ECMAScript2015，2015-6月正式发布，向下兼容ES5.1
    * ES6来编写Node.js程序
    * ES6让JavaScript语言能够开发复杂应用程序
- 严格模式
    * ES5中出现的模式
    * 严格模式的目的：
        - 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
        - 消除代码运行的一些不安全之处，保证代码运行的安全；
        - 提高编译器效率，增加运行速度；
        - 为未来新版本的Javascript做好铺垫
        - 参考
            [严格模式的限制](https://jsmean.com/blog/post/55a9db88a0367a75336e8884)

            [严格模式的限制](http://www.cnblogs.com/jiqing9006/p/5091491.html)

    * 开启严格模式
        - 在作用域的最上面  "use strict"
            * js文件的最开头
            * function的开头
- 变量和常量
    * 变量 let
        - 没有变量提升，必须先定义再使用
        - 有块级作用域
        - 解决问题

        ```javascript
        window.onload = function () {
                    var ul = document.getElementById("list");

                    var lis = ul.getElementsByTagName("li");

                    for(let i = 0, length=lis.length; i < length; i--) {

        //                (function (i) {
        //                    lis[i].onclick = function () {
        //                        console.log(i);
        //                    }
        //                })(i);

                        lis[i].onclick = function () {
                            console.log(i);
                        }
                    }
                }
        ```

    * 常量 const
        - 常量一旦赋值，不能改变
        - 有块级作用域
        - 没有变量提升，先定义再使用
        - 不可以重复定义
        - 必须有初始值，否则报错

        - 在Node.js中，所有接收require()获得的对象都使用const修饰
- string的扩展方法
    * includes()   返回布尔值，是否包含，第二个参数从第几个位置开始查找
    * startsWith() 返回布尔值，是否以...开头，第二个参数从第几个位置开始查找
    * endsWith()   返回布尔值，是否以...结尾，第二个参数, 前n个字符以...结尾
    * repeat()     重复次数
- 模板
    * 示例1：
    ```javascript
    let name = "steve jobs";
    let str = `hello ${name}`;
    ```
    * 示例2：
    ```
    let obj = {name:"jobs", age: 18, salary: 1};

    let template = `
        姓名：${obj.name}
    年龄：${obj.age}
    工资：${obj.salary}
    `.trim();
    ```

    * 示例3：生成页面

- 箭头函数 
    * 格式： => (读作：goesto)  左边是参数，右边是方法体
    * 演变：function f(x,y) {}  ----->  演变成箭头函数
           (x, y) => {}
           语法格式简单
    * 箭头函数的几种形式：
        - 没有参数 () => console.log("hello");
        - 有一个参数  a => --a;
        - 有多个参数  (a,b) => a - b;

        - 方法体有多条语句  (a,b) => { a=1; b=2; console.log(a-b)};
    * 箭头函数的注意事项
        - 箭头函数不会影响this的指向
        - 箭头函数根本没有自己的this，箭头函数内部的this就是外层代码块的this
        - 箭头函数中没有arguments对象，箭头函数内部的arguments指向外层函数的arguments
        - 不可以当做构造函数

- Promise

Promise为了解决回调地狱(callback hell)
Promise是一个容器，容器中有三种状态
    Pending  默认，进行中
    Resolved 已完成
    Rejected 已失败

+ 演示1 promise基本使用

```
new Promise((resolved, rejected) => {
  fs.readFile('12.txt', (err, data) => {
    if(err) {
      rejected(err);
    }
    resolved(data);
  })
}).then((data) => {
  console.log(data.toString());
}, (err) => {
  console.log(err);
})
```

+ 演示2  封装promise对象

```
function readFile(filePath) {
    return new Promise((resolved, rejected) => {
        fs.readFile(filePath, (err, data) => {
            if (err) {
                rejected(err);
            }
            resolved(data);
        })
    });
}


readFile('4.txt')
    .then((data) => {
        console.log(data.toString());
        return readFile('2.txt');
    })
    .then((data) => {
        console.log(data.toString());
        return readFile('3.txt');
    })
    .then((data) => {
        console.log(data.toString());
    })
    .catch((err) => {
        console.log(err);
    })
```

- ES6的学习站点
    * 各个浏览器对ES6的支持
        http://kangax.github.io/compat-table/es6/
    * 学习站点
        http://es6.ruanyifeng.com/#README
