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

~~~
Node.js 是一种建立在Google Chrome's V8 引擎上的non-blocking(非阻塞),event-driven(基于事件的)I/O平台。Node.js平台使用的开发语言是JavaScript，平台提供了操作系统底层的API，方便做服务器端编程，
具体包括：文件操作、进程操作、通信操作等系统模块，支持模块化的开发
~~~


C/S
- 服务端server
- 客户端client

B/S
browser 浏览器
server  服务器




## Node 可以做什么

- 高性能的网站服务器
- 简单易用的命名行应用程序
+ gulp、less
+ i5ting
    https://github.com/i5ting/tocmd.npm
+ browser-sync
    http://www.browsersync.cn/

- 实时多人游戏后台服务器
- 高大上的桌面应用程序
    electron

+ 使用 Web 技术 作为解决方案
- 底层的物联网开发
- 移动开发
+ 使用 Web 技术作为解决方案

## 安装Node.js

查看Node是否安装成功/查看Node的当前版本
    node -v

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
    两边以 **英文分号** 进行分隔。

例如 `feiq.exe` 程序的绝对路径是 `C:\Program Files\feiQ`，
则在 `path` 中添加 `;C:\Program Files\feiQ;`

二：也可以在外部先定义一个变量名，值就是程序所属目录的绝对路径，
    然后在 path 中以 `%变量名%` 的方式引入，两边以分号分隔

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
    
+ 相对路径，相对于当前编写的文件查找文件
    fs.readFile('./statics/css/style.css',....); 
+ 根路径，在当前文件所处的跟目录查找文件，c:/statics/css.....
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


+ MIME模块

https://github.com/broofa/node-mime


在当前项目使用npm安装第三方包
1、在当前项目文件夹 打开命令窗口  输入  npm init /  npm init -y   创建了package.json
2、安装包   npm install 包名  --save(在package.json中记录依赖)

## 模板引擎 xtpl

## 封装render方法