---
layout: post
title: "Mongoose"
date: 2018-04-3
description: "Mongoose基本用法"
tag: mongodb
---   


`Mongoose`：是在node.js异步环境下对mongodb进行便捷操作的对象模型库，封装了MongoDB对文档的的一些增删改查等常用方法。

- `Schema`：数据库模型模型骨架，每一个Schema对应数据库的一个集合(表)<br>
Schema定义了集合中文档的样式。
- `model`：由Schema构造而成的，具有抽象属性和行为，可实例化。
- `Instance`：有model创建的实例，每个实例就是一个document(行)。 

## 一、基本操作

### 连接数据库

1）启动服务器：

	F:\mongoDB\bin\mongod --dbpath F:\data\db

2）连接本地的test数据库

	var mongoose = require('mongoose');

	var db = mongoose.connect("mongodb://127.0.0.1:27017/test");

	db.connection.on("error", function (error) {
    	console.log("数据库连接失败：" + error);
	});

	db.connection.on("open", function () {
   		console.log("------数据库连接成功！------");
	});

### Schema

`Schema`：一种以文件形式存储的`数据库模型骨架`，无法直接通往数据库端，也就是说它不具备对数据库的操作能力，仅仅只是数据库模型在程序片段中的一种表现，可以说是数据属性模型(传统意义的表结构)，又或着是"集合"的模型骨架。

	var mongoose = require("mongoose");

	var TestSchema = new mongoose.Schema({

    	name : { type:String },//属性name,类型为String
    	age  : { type:Number, default:0 },//属性age,类型为Number,默认为0
    	time : { type:Date, default:Date.now },
    	email: { type:String,default:''}

	});

 *注：Schema定义集合结构（定义表的列）*

### Model--操作数据库--创建集合

	//引入数据库模块
	var mongoose = require("mongoose");

	//连接本地名为test的数据库
	//var db = mongoose.connect("mongodb://user:pass@localhost:port/database");
	var db = mongoose.connect("mongodb://127.0.0.1:27017/test");

	//用Schema定义集合结构
	var TestSchema = new mongoose.Schema({
    	name : { type:String },
    	age  : { type:Number, default:0 },
    	email: { type:String },
    	time : { type:Date, default:Date.now }
	});

	//创建model,在内存中创建结构为TestSchema名为test1的集合
	var TestModel = db.model("test1", TestSchema );

	//插入数据到内存中的test1集合
	var TestEntity = new TestModel({
    	name : "helloworld",
    	age  : 28,
    	email: "helloworld@qq.com"
	});

	//将TestEntity写入到数据库中
	TestEntity.save(function(error,doc){
  	if(error){
    	console.log("error :" + error);
  	}else{
     	console.log(doc);
  	}
	});

> Schema：数据库集合的模型骨架，或者是数据属性模型传统意义的表结构。<br>
> Model ：通过Schema构造而成，除了具有Schema定义的数据库骨架以外，还可以具体的操作数据库。<br>
> Entity：通过Model创建的实体，它也可以操作数据库。

## 二、增删改查

### find()查询

find查询：`obj.find(查询条件,callback)`;

	Model.find({},function(error,docs){
   	//若没有向find传递参数，默认的是显示所有文档
	});

	Model.find({ "age": 28 }, function (error, docs) {
 	 if(error){
    	console.log("error :" + error);
 	 }else{
    	console.log(docs); //docs: age为28的所有文档
	}
	});

find过滤查询：

	//返回只包含一个键值name、age的所有记录
	Model.find({},{name:1, age:1, \_id:0}，function(err,docs){
   		//docs 查询结果集
	})
说明：需要显示的属性设置为大于0的数，_id默认返回，不显示要加\_id:0。

- findOne查询 ：只返回符合条件的首条文档数据。
- findById查询：根据文档_id来查询文档。

### Model.create()保存

`Model.create(文档数据, callback))`

	Model.create({ name:"model\_create", age:26}, function(error,doc){
    	if(error) {
        	console.log(error);
    	} else {
        	console.log(doc);
    	}
	});

### Entity.save()保存

`Entity.save(文档数据, callback))`

	//1.通过model创建entity实体，Model构造函数传入文档数据
	//2.再entity.save()

	var Entity = new Model({name:"entity\_save",age: 27});

	Entity.save(function(error,doc) {
	  if(error) {
        	console.log(error);
    	} else {
        	console.log(doc);
    	}
	});

model调用的是create方法，entity调用的是save方法

### update()数据更新

`obj.update(查询条件,更新对象,callback);`

	var conditions = {name : 'test\_update'};//条件
	var update = {$set : { age : 16 }};//操作

	TestModel.update(conditions, update, function(error){
    	if(error) {
        	console.log(error);
    	} else {
        	console.log('Update success!');
    	}
	});

### remove()删除数据

`obj.remove(查询条件,callback);`

	var conditions = { name: 'tom' };
	TestModel.remove(conditions, function(error){
   		if(error){
      	 	console.log(error);
    	} else {
        	console.log('Delete success!');
    	}
	});

>查询：find查询返回符合条件一个、多个或者空数组文档结果。<br>
保存：model调用create方法，entity调用的save方法。<br>
更新：obj.update(查询条件,更新对象,callback)，根据条件更新相关数据。<br>
删除：obj.remove(查询条件,callback)，根据条件删除相关数据。

## 三、高级查询

### 大于、小于、等于、不等于

- `$gt`：大于
- `$lt`：小于
- `$lte`：小于等于
- `$gte`：大于等于
- `$ne`：不等于
- `$in`：包含、等于

示例：

    Model.find({"age":{"$gt":18}},function(error,docs){
          //查询所有age大于18的数据
    });

    Model.find({ age:{ $in: 20}},function(error,docs){
          //查询age等于20的所有数据
    });

    Model.find({ age:{$in:[20,30]}},function(error,docs){
         //可以把多个值组织成一个数组
    });

### 或者
`$or`

    Model.find({"$or":[{"name":"yaya"},{"age":28}]},function(error,docs){
         //查询name为yaya或age为28的全部文档
    });

### 存在
`$exists`

    Model.find({name: {$exists: true}},function(error,docs){
         //查询所有存在name属性的文档
    });

    Model.find({telephone: {$exists: false}},function(error,docs){
         //查询所有不存在telephone属性的文档
    });

### 游标
数据库使用游标返回find的执行结果，客户端对游标的实现通常能够对最终结果进行有效的控制。

`find(Conditions,fields,options,callback);`

1）limit：限制返回结果的数量。

    Model.find({},null,{limit:20},function(err,docs){
         console.log(docs);
    });

2）skip：略过指定的返回结果数量。

	Model.find({},null,{skip:4},function(err,docs){
	    console.log(docs);
	});

3）sort：对返回结果进行有效排序。1是升序，-1是降序。

    Model.find({},null,{sort:{age:-1}},function(err,docs){
         //查询所有数据，并按照age降序顺序返回数据docs
    });

## 四、属性方法

### 创建实例方法

    var mongoose = require('mongoose');

    var saySchema = new mongoose.Schema({name : String});

    saySchema.method('say', function () {
         console.log('Trouble Is A Friend');
    })

    var say = mongoose.model('say', saySchema);

    var lenka = new say();//实例化model

    lenka.say(); //Trouble Is A Friend

### Schema静态方法

    var mongoose = require("mongoose");

    var db = mongoose.connect("mongodb://127.0.0.1:27017/test");

    var TestSchema = new mongoose.Schema({
          name : { type:String },
          age  : { type:Number, default:0 },
          email: { type:String, default:"" },
          time : { type:Date, default:Date.now }
    });

    TestSchema.static('findByName', function (name, callback) {
          return this.find({ name: name }, callback);
    });

    var TestModel = db.model("test1", TestSchema );

    TestModel.findByName('tom', function (err, docs) {
        //docs所有名字叫tom的文档结果集
    });

### Schema追加方法

	var mongoose = require("mongoose");
    var db = mongoose.connect("mongodb://127.0.0.1:27017/test");

    var TestSchema = new mongoose.Schema({
           name : { type:String },
           age  : { type:Number, default:0 },
           email: { type:String, default:"" },
           time : { type:Date, default:Date.now }
    });

	TestSchema.methods.speak = function(){
           console.log('我的名字叫'+this.name);
    }

    var TestModel = db.model('test1',TestSchema);

    var TestEntity = new TestModel({name:'Lenka'});

    TestEntity.speak();//我的名字叫Lenka
