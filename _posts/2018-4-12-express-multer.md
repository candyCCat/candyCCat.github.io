---
layout: post
title: "Node模块：multer"
date: 2018-04-12
description: "multer模块使用问题"
tag: Node
---  
### multer

multer的作用：是一个nodejs的中间件，用于处理`multipart/form-data`数据，上传文件。

**注意**: Multer 不会处理任何非 multipart/form-data 类型的表单数据。

### Error1：multer 版本问题
node运行时出现如下错误：

	throw new TypeError('app.use() requires a middleware function')
	
	TypeError: app.use() requires a middleware function
	    at Function.use (F:\GitHub\my-easy-eshop\node_modules\express\lib\application.js:210:11)
	    at Object.<anonymous> (F:\GitHub\my-easy-eshop\temp.js:37:5)
	    at Module._compile (module.js:652:30)
	    at Object.Module._extensions..js (module.js:663:10)
	    at Module.load (module.js:565:32)
	    at tryModuleLoad (module.js:505:12)
	    at Function.Module._load (module.js:497:3)
	    at Function.Module.runMain (module.js:693:10)
	    at startup (bootstrap_node.js:188:16)
	    at bootstrap_node.js:609:3

- 分析：究其源头，主要出错在`app.use(multer());`这句话；
- 原因：报错是因为版本问题，我下载的是`1.3.0`版本，已经不能`app.use(multer());`这样写了；
- 解决方法：
	1. 使用0.1.8（或者0.几的版本）
	2. 探索新写法

### Error2：post请求头Content-Type问题

四种常见的`POST`提交数据方式：

1.application/x-www-form-urlencoded：

	var data="name="+name+"&password"=password;

2.application/json：

	var data=JSON.stringify({name:username,password:password});
	//将字JSON格式转化为JSON字符串

3.text/xml

4.multipart/form-data：

这种方式用于：使用表单上传文件时，让`form`的`enctyped`属性等于这个值。<br>
提交表单的过程中遇到了以下几个错误：

**第一步纠错**：在使用`原生ajax`发送post请求时，设置`Content-Type`：

	//设置编码
    request.setRequestHeader('Content-Type','multipart/form-data');

node端出现error：

	Error: Multipart: Boundary not found
	    ………………

根据博文：<https://www.cnblogs.com/yydcdut/p/3736667.html> ：
>以multipart/form-data编码的POST请求格式与application/x-www-form-urlencoded完全不同，multipart/form-data需要首先在HTTP请求头设置一个分隔符，例如ABCD：

>httpURLConnection.setRequestProperty("Content-Type", "multipart/form-data;boundary=ABCD");

分析推测：可能是没在请求头设置中加上`boundary=……`的设置，加上之后`Error: Multipart: Boundary not found`的错误提示没有了

	request.setRequestHeader('Content-Type','multipart/form-data;boundary=ABC');

**第二步纠错**：

出现错误：服务端收到通过post请求传来的数据`req.body={}`、`req.file=undefined`；

解决：客户端请求去除：`request.setRequestHeader()`的设置。

**第三步纠错**：

node端出现error：

	Error: Unexpected field
		………………

原因是：从客户端传到服务端的文件信息包含字段`fieldname`（Field name 由表单指定）,而服务器端在调用`upload.single(filedname)`时，传入参数filedname与表单中的name不一致，导致这个错误。

*至此，浏览器与服务端文件传输正常。*

### 实例：原生AJAX的POST请求上传文件

	var btn=document.getElementById("submit");
	var fileM=document.getElementById("file");
	btn.onclick=function(){
		var formData = new FormData();
		var fileObj=fileM.files[0];//file对象
		formData.append('file',fileObj);
        formData.append('name','huxu');
		formData.append('gender','1');//可以append多个项
	
		var request=new XMLHttpRequest();
	    request.open("POST",url,true);
		request.send(formData);
		request.onload=function(){
		    if(request.status==200){
		    	console.log("成功")
		    }
		    else{
		   		console.log(request.responseText);
		    }
	    }
	}

也可以直接传递表单：

	var btn=document.getElementById("submit");
    var form=document.getElementById("form");
	btn.onclick=function(){
		var request=new XMLHttpRequest();
	    request.open("POST",url,true);
		request.send(new FormData(form));
		request.onload=function(){
              //code……
        }
	}

## 1.3.0版本multer用法

### multer与body-parser比较

- body-parser：<br>
解析以：`application/x-www-form-urlencoded`和`application/json`格式发送而来的参数；<br>
参数在服务端调用：`req.body`（其中req是express的request对象）

- multer：<br>
解析以：`multipart/form-data`格式发送而来的参数，其中包括文本域字段和文件对象；<br>
参数调用：
	- `req.body`：body 对象包含表单的文本域信息；
	- `req.file`：当表单中只有一个文件时，file包含表单上传的单个文件信息；
	- `req.files`：当表单中包含多个文件，有files对象。

### 基本用法

	var express = require('express')
	var multer  = require('multer')
	var upload = multer({ dest: 'uploads/' })//dest指定文件上传的路径
	
	var app = express()
	
	app.post('/profile', upload.single('file'), function (req, res, next) {
	  // 传入的'file'是表单中上传文件标签的name属性值
	  // req.file 上传的文件的信息
	  // req.body 将具有文本域数据，如果存在的话
	})
	
	app.post('/photos/upload', upload.array('photos', 12), function (req, res, next) {
	  // req.files 是 `photos` 文件数组的信息
	  // 12是限制上传文件的数量
	  // req.body
	})
	
	var cpUpload = upload.fields([{ name: 'avatar', maxCount: 1 }, { name: 'gallery', maxCount: 8 }])
	app.post('/cool-profile', cpUpload, function (req, res, next) {
	  // req.files 是一个对象 (String -> Array) 键是文件名，值是文件数组
	  //
	  // 例如：
	  //  req.files['avatar'][0] -> File
	  //  req.files['gallery'] -> Array
	  //
	  // req.body 将具有文本域数据，如果存在的话
	})

### 文件对象包含的字段信息

|Key|Description|Note|
|-|-|
|fieldname|	Field name 由表单指定	||
|originalname|	用户计算机上的文件的名称||
|encoding|	文件编码	||
|mimetype|	文件的 MIME 类型	||
|size	|文件大小（字节单位）	||
|destination|	保存路径	DiskStorage||
|filename	|保存在 destination 中的文件名	|DiskStorage|
|path	|已上传文件的完整路径	|DiskStorage|
|buffer	|一个存放了整个文件的Buffer	|MemoryStorage|

### multer(options)

|Key	|Description|
|-|-|
|dest or storage	|在哪里存储文件|
|fileFilter	|文件过滤器，控制哪些文件可以被接受|
|limits	|限制上传的数据|
|preservePath	|保存包含文件名的完整文件路径|

### storage:控制文件存储路径及文件名

`multer.diskStorage()`：

	var storage = multer.diskStorage({
	  destination: function (req, file, cb) {
	    cb(null, '/tmp/my-uploads')
	  },
	  filename: function (req, file, cb) {
	    cb(null, file.originalname+ '-' + Date.now()+'jpg')
	  }
	})
	
	var upload = multer({ storage: storage })

### fileFilter:控制文件是否上传

	var upload=multer({
	    storage:storage,
	    fileFilter:function(req,file,cd){
		  // 拒绝这个文件，使用`false`，像这样:
		  cb(null, false)
		
		  // 接受这个文件，使用`true`，像这样:
		  cb(null, true)
		
		  // 如果有问题，你可以总是这样发送一个错误:
		  cb(new Error('I don\'t have a clue!'))
	    }
	 });