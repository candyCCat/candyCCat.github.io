---
layout: post
title: "mongoDB学习笔记"
date: 2018-04-3
description: "mongoDB的安装及基本操作"
tag: mongodb
---   
![](/images/posts/180402/mongoDB-logo.png)
## 一、简介

### NoSQL
- NoSQL(Not Only SQL)非关系型的数据库。
- NoSQL用于超大规模数据的存储。（例如谷歌或Facebook每天为他们的用户收集万亿比特的数据）。这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展。
- 强调Key-Value Stores和文档数据库；
- 根据`CAP定理`将 NoSQL 数据库分成了满足CA原则、满足CP原则和满足AP原则三大类。
	- CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，最多只能同时较好的满足两个。

### MongoDB
- 基于`分布式文件存储`的开源数据库，旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。
- 介于关系数据库和非关系数据库之间。
- MongoDB 将数据存储为一个文档，数据结构由键值`(key=>value)`对组成。MongoDB 文档类似于 `JSON`对象。字段值可以包含其他文档，数组及文档数组。

## 二、安装及操作

### README

- components 核心组件
	- mongod - The database server.<br>
	数据库服务器
	- mongos - Sharding router.<br>
	分片路由
	- mongo  - The database shell (uses interactive javascript).<br>
	数据库控制外壳（用JavaScript作为交互语言）
- utilities 工具
	- mongodump - Create a binary dump of the contents of a database.<br>
	数据库内容的二进制转存
	- mongorestore - Restore data from the output created by mongodump.<br>
	转存还原
	- mongoexport - Export the contents of a collection to JSON or CSV.<br>
	将集合的内容导出为JSON或CSV。
	- mongoimport - Import data from JSON, CSV or TSV.<br>
	从JSON，CSV或TSV导入数据
	- mongofiles - Put, get and delete files from GridFS.<br>
	从GridFS中存放、取得、删除文件
		- `GridFS`：用于存储和恢复那些超过16M（BSON文件限制）的文件；GridFS 也是文件存储的一种方式，但是它是存储在MonoDB的集合中。
	- mongostat - Show the status of a running mongod/mongos.<br>
	实时状态显示
	- bsondump - Convert BSON files into human-readable formats.<br>
	将BSON格式转换为人类可读格式。
	- mongoreplay - Traffic capture and replay tool.<br>
	流量捕获和存放工具
	- mongotop - Track time spent reading and writing data.<br>
	跟踪读取或者写入数据的时间

### 安装及配置
1）启动服务器

- **创建数据存储目录**-->MongoDB将数据存储在db目录下。（这个数据目录不会自动创建）<br>
我在F盘目录下：`mkdir data`-->`cd data`-->`mkdir db`
- **运行mongoDB服务器**：<br>
`F:\mongoDB\bin\mongod --dbpath F:\data\db`
- **连接mongoDB**，在命令行中运行mongo.exe：
`F:\mongoDB\bin\mongo.exe`

2）配置MongoDB服务

- **创建日志目录**：<br>
`mkdir F:\data\log`
- **创建配置文件**：
	- 创建一个位于：`F:\mongoDB\mongod.cfg`的配置文件；
	- 指定`systemLog.path`和`storage.dbPath`；

配置内容：

	systemLog:
	    destination: file
	    path: f:\data\log\mongod.log
	storage:
	    dbPath: f:\data\db

- **安装MongoDB服务**：<br>
`F:\mongoDB\bin\mongod.exe --config "f:\mongoDB\mongod.cfg" --install`
- **启动MongoDB服务**：<br>
`net start MongoDB`
- **关闭MongoDB服务**：<br>
`net stop MongoDB`
- **移除MongoDB服务**：<br>
`F:\mongodb\bin\mongod.exe --remove`

	*注：命令行下运行 MongoDB 服务器 和 配置 MongoDB 服务 任选一个方式启动就可以。*

3）MongoDB后台管理`Shell`

- MongoDB Shell：是MongoDB自带的交互式Javascript shell，用来对MongoDB进行操作和管理的交互式环境。

当你进入mongoDB后台后，它默认会链接到`test 文档`（数据库）：

	F:\mongoDB\bin>mongo
	MongoDB shell version v3.6.3
	connecting to: mongodb://127.0.0.1:27017
	MongoDB server version: 3.6.3
	Server has startup warnings:
	2018-04-03T12:13:55.034+0800 I CONTROL  [initandlisten]
	2018-04-03T12:13:55.034+0800 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
	2018-04-03T12:13:55.035+0800 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
	2018-04-03T12:13:55.038+0800 I CONTROL  [initandlisten]
	2018-04-03T12:13:55.040+0800 I CONTROL  [initandlisten] ** WARNING: This server is bound to localhost.
	2018-04-03T12:13:55.042+0800 I CONTROL  [initandlisten] **          Remote systems will be unable to connect to this server.
	2018-04-03T12:13:55.045+0800 I CONTROL  [initandlisten] **          Start the server with --bind_ip <address> to specify which IP
	2018-04-03T12:13:55.047+0800 I CONTROL  [initandlisten] **          addresses it should serve responses from, or with --bind_ip_all to
	2018-04-03T12:13:55.050+0800 I CONTROL  [initandlisten] **          bind to all interfaces. If this behavior is desired, start the
	2018-04-03T12:13:55.053+0800 I CONTROL  [initandlisten] **          server with --bind_ip 127.0.0.1 to disable this warning.
	2018-04-03T12:13:55.055+0800 I CONTROL  [initandlisten]
	2018-04-03T12:13:55.058+0800 I CONTROL  [initandlisten]
	2018-04-03T12:13:55.060+0800 I CONTROL  [initandlisten] ** WARNING: The file system cache of this machine is configured to be greater than 40% of the total memory. This can lead to increased memory pressure and poor performance.
	2018-04-03T12:13:55.063+0800 I CONTROL  [initandlisten] See http://dochub.mongodb.org/core/wt-windows-system-file-cache
	03T12:13:55.065+0800 I CONTROL  [initandlisten]
	>

如上安装成功。

### MongoDB Shell基本操作
1、创建数据库：

	> show dbs -->查看所有数据库
	admin   0.000GB
	config  0.000GB
	local   0.000GB
	test    0.000GB

	> use test -->连接到指定数据库/创建数据库
	switched to db test

	> db -->显示当前数据库对象或者集合
	test

2、删除数据库

	> db.dropDatabase()
	{ "dropped" : "test", "ok" : 1 }


3、创建集合

	> db.createCollection("runoob")
	{ "ok" : 1 }

	> show collections或者tables -->查看数据库中的集合
	runoob

4、删除集合

	> db.collectionName.drop()

5、插入文档

使用`insert()`或者`save()`方法

	> db.runoob.insert({age:"22",name:"xuxu",gender:"girl"})
	WriteResult({ "nInserted" : 1 })

	> db.runoob.find()
	{ "_id" : ObjectId("5ac3314316b3660d529500b9"), "age" : "22", "name" : "xuxu", "gender" : "girl" }

	#  插入单条数据
	> var document = db.collection.insertOne({"a": 3})
	> document
	{
	        "acknowledged" : true,
	        "insertedId" : ObjectId("571a218011a82a1d94c02333")
	}

	#  插入多条数据
	> var res = db.collection.insertMany([{"b": 3}, {'c': 4}])
	> res
	{
	        "acknowledged" : true,
	        "insertedIds" : [
	                ObjectId("571a22a911a82a1d94c02337"),
	                ObjectId("571a22a911a82a1d94c02338")
	        ]
	}

6、更新文档

使用`update()`或者`save()`方法

db.collection.updateOne() 向指定集合更新单个文档<br>
db.collection.updateMany() 向指定集合更新多个文档

7、删除文档

`remove()`

	#删除col集合中的左右数据
	>db.col.remove({})

	#删除col中一行数据
	>db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)

	#删除符合条件的数据
	>db.col.remove({'title':'MongoDB 教程'})
	WriteResult({ "nRemoved" : 2 })           # 删除了两条数据

`deleteOne()`和`deleteMany()`方法

	如删除集合下全部文档：
	db.inventory.deleteMany({})

	删除 status 等于 A 的全部文档：
	db.inventory.deleteMany({ status : "A" })

	删除 status 等于 D 的一个文档：
	db.inventory.deleteOne( { status: "D" } )

8、查询文档

	>db.col.find()
	>db.col.find().pretty() #易读的方式


|操作|范例|RDBMS中的类似语句|
|-|-|-|
|等于|db.col.find({"by"："菜鸟教程"}).pretty()|where by = '菜鸟教程'|
|小于|db.col.find({"likes":{`$lt`：50}}).pretty()|where likes < 50|
|小于或等于|	db.col.find({"likes":{`$lte`：50}}).pretty()|where likes <= 50|
|大于|	db.col.find({"likes":{`$gt`；50}}).pretty()|where likes > 50|
|大于或等于|	db.col.find({"likes":{`$gte`：50}}).pretty()|where likes >= 50|
|不等于|	db.col.find({"likes":{`$ne`：50}}).pretty()|where likes != 50|
|OR|db.col.find({`$or`：[{key1: value1}, {key2:value2}]}).pretty()||
|AND和OR联合使用|db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()||

9、条件操作符

### 概念

|SQL术语/概念|MongoDB术语/概念|解释/说明|
|-|-|-|
|database|database|数据库|
|table|collection|数据库表/集合|
|row|document|数据记录行/文档|
|column	|field|数据字段/域|
|index|index|索引|
|table joins||表连接,MongoDB不支持|
|primary key|primary key|主键,MongoDB自动将`_id`字段设置为主键|

#### 文档

- 文档：是一组键值(key-value)对(即BSON)。
- 文档中的键/值对是有序的。

#### 集合

类似于关系型数据库中的表格

**capped collections**：

- 固定大小的collection；
- 是高性能自动的维护对象的插入顺序。
- 必须要显式的创建一个capped collection， 指定一个collection的大小，单位是字节。collection的数据存储空间值提前分配的：<br>
`db.createCollection("mycoll", {capped:true, size:100000})`
