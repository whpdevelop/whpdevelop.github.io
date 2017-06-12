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

show dbs  		查看所有数据库
db 		  		查看当前数据库
use 数据库名称	切换数据库(如果数据库不存在会自动创建)
db.dropDatabase()   删除数据

- 增删改查命令

+ 插入文档
db.集合名称.insert(document);

示例：
db.students.insert({name: "张三", age: 18})

+ 更新文档

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
	upsert: true
});


//$set 修饰要更新的域，如果不存在则创建
db.students.update({name: "张三"}, {$set: {age: 20}}, {
	upsert: true
});

//修改所有匹配的结果
db.students.update({name: "张三"}, {$set: {age: 20}}, {
	multi: true
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


 

+ save方法

db.集合名称.save(document)
不指定_id，类似insert
指定_id，类似update
db.studetns.save({
	"_id" : ObjectId("56064f89ade2f21f36b03136"),
	………………
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
		throw err;
	}
	//进行数据库操作

	//关闭数据库
	db.close();
});

- 插入数据

+ 插入数据

//获取集合
var students = db.collection('students');
//插入一条数据
students.insertOne({name: '刘备', age: 18}, function(err, result) {
	if(err) {
		throw err;
	}
	console.log(result);
});

//插入多条数据
students.insertMany([
	{name: '李四', age: 19},
	{name: '王五', age: 20}
], function (err, result) {
	if(err) {
		throw err;
	}
	console.log(result);
})


+ 更新数据

//更新一条数据
students.updateOne({name: '刘备'}, {$set: {age: 20}}, function(err, result) {
	if(err) {
		throw err;
	}
	console.log(resu);
})


//更新多条数据
students.updateMany({name:'abc'}, {$set: {age: 111}}, {multi: true}, function(err, result) {
	if(err) {
		throw err;
	}
	console.log(result);
})

+ 删除数据

students.deleteOne({name:'abc'},  function(err, result) {
	if(err) {
		throw err;
	}
	console.log(result);
})


students.deleteMany({name:'abc'},  function(err, result) {
	if(err) {
		throw err;
	}
	console.log(result);
})


+ 查询数据

students.find({name:'李四'}).toArray(function(err, result) {
	console.log(result);
})

students.find().toArray(function(err, result) {
	console.log(result);
})



+ 根据id查询一条数据

var ObjectID = require('mongodb').ObjectID;
posts.findOne({_id: ObjectID('58abf1bfc692de395ccdd2b0')}, function(err, data) {
	console.log(data);
});