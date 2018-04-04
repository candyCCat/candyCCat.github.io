---
layout: post
title: "express--app.use，app.get，route.get方法解析"
date: 2018-04-4
description: "express框架中，app.use、app.get、router.get等方法的辨析，帮助理解"
tag: Node-express
---   

**前言**：近来学习nodejs的web框架express，遇到app.use、app.get、router.get等方法，理解比较混乱，特地总结此博文，以理清思路。

### 结论

- `app.use(path,callback)`中的callback既可以是router对象又可以是函数
- `app.get(path,callback)`中的callback只能是函数
- `router.get(path,callback)`：为路由对象router新建一个路由，需要用`app.use(path,router)`绑定路由规则。

### 什么时候用？

- 用`express.Router()`可以创建路由对象router，一个路由对象可以有多个路由规则。
- 由`app.use(path，router)`将多个路由规则挂载到应用路径。
- 如果一个路由对象只有一条规则，则可直接用app.get或者app.use写回调函数；如果一个路由有多条规则，则可用到路由对象router。

### 为什么出现路由对象？

- 使用`express.Router`类来创建可挂载的、模块化的路由处理程序
- `Router`实例是一个完整的中间件和路由系统

### 例子

	var express = require('express');
	var app = express();
	var router=express.Router();

	//1、app.get()
	app.get('/home1',function(req,res,next){
	    res.send('hello home1!');
	});

	//2、app.use()
	app.use('/home2',function(req,res,next){
	    res.send('hello home2!');
	});

	//3、router.get()
	router.get('/',function(req,res,next){
	    res.send('hello about!');
	});
	router.get('/home3',function(req,res,next){
	    res.send('hello home3!');
	});
	app.use('/about',router);
	//访问：/about和/about/home3
