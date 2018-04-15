---
layout: post
title: "node知识点"
date: 2018-04-10
description: ""
tag: Node
---

# 持续更新

## 零碎点

### 定义全局变量
`global.dbHelper = require( './common/dbHelper' )`：这样dbHelper就可以在任何模块内调用。

`global.db = mongoose.connect("mongodb://127.0.0.1:27017/test")`：数据库的连接也需要定义全局变量

### node.js文件中：console.log中文乱码问题

问题：node的`.js`文件中，当`console.log("中文")`时，控制台输出会出现乱码现象。

原因：`.js`文件是以GBK的编码格式保存，？？至于为什么暂时没理清内因，待续…………

解决方法：确保`.js`文件是tuf-8编码格式

### express路由中的路由转跳

`res.render`(静态页面)：渲染，返回需要渲染的页面；
`res.redirect`(路由路径)：重定向，在路由中实现路由转跳（一般转跳到响应路径的`get`路由）。

### <%- %>、<%= %>

在html中`<%-变量%>`、`<%=变量%>`能直接在页面中展现从后天接收到的数据，它们两的区别在于：

`<%=变量%>`：会被escapge转义编码 

`<%-变量%>`：输出原始内容, 不会被escape

### javascript中：判断一个对象是否为空的方法

	
	var obj={};
	if(obj){
		console.log("if-obj为真true");
	};

因此，判断一个对象是否为空的方法：

`JSON.stringify()`：将其转换为JSON字符串再判断，如果为空：

	JSON.stringify(data) === '{}'//为true

**在操作mongodb数据库时，判断一个集合是否为空**：

	JSON.stringify(docs) === '[]'

### node中删除文件及文件夹的方法

删除文件：

	var fs = require('fs');
	fs.unlink(path,callback);

删除文件夹：

	var fs = require('fs');
	deleteFolder(path);
    function deleteFolder(path) {
        var files = [];
        if( fs.existsSync(path) ) {
            files = fs.readdirSync(path);
            files.forEach(function(file,index){
                var curPath = path + "/" + file;
                if(fs.statSync(curPath).isDirectory()) { // recurse
                    deleteFolder(curPath);
                } else { // delete file
                    fs.unlinkSync(curPath);
                }
            });
            fs.rmdirSync(path);
        }
    }