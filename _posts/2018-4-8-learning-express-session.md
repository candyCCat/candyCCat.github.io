---
layout: post
title: "Node模块：express-session"
date: 2018-04-08
description: "nodejs模块：express-session学习笔记"
tag: Node
---  

## Session

### 为什么有session？

&emsp;&emsp;Internet通过协议分为`stateful`和`stateless`两类，而http是`stateless`协议，客户端发送请求到服务端建立一个连接，请求得到响应后连接即中断，服务器端不会记录状态，因此服务器端想要确定是哪个客户端提交过来的请求，就必须要借助一些东西去完成：session和cookies。

### session是什么？

&emsp;&emsp;`session`即`会话`，在web应用中，session是记录客户状态的机制，不同于Cookie是保存在浏览器端，**session是保存在服务器上的**。

&emsp;&emsp;客户端浏览器访问服务器时，服务器把客户信息以某种形式记录在服务器上，客户端浏览器再次访问服务器时，就可以直接从该`session`中查找客户状态。

### session的原理

基本原理是：当浏览器访问服务器并发送第一次请求时，服务器端一个创建session对象，每一个session维护一份**会话信息数据**，而客户端和服务端依靠一个**全局唯一的标识**来访问会话信息数据。

1. 生成全局唯一标识符（`sessionid`）
2. 开辟数据存储空间；
3. 将session的全局唯一标示符发送给客户端。

问题关键：**服务器和客户端如何交流session的唯一标识符**。<br>
常用方法有：`cookie`和`URL重写`。

### session的大致工作流程

1. 用户提交包含用户名及密码的表单，发送HTTP请求；
2. 服务器验证用户发来得用户名和密码；
3. 如果正确，则把当前用户相关信息储到session的会话数据中，并生成`sessionid`；
4. 设置cookie为sessionId=xxxxxx并发送HTTP响应；
5. 用户收到HTTP响应后，得到这个`sessionid`，在此后的请求中发送带有该`sessionid`的Cookie给服务器；
6. 服务器收到此后的HTTP请求后，发现Cookie中有`sessionid`，进行防篡改验证；
7. 如果通过验证，根据该`sessionid`可以取出对应的该用户信息，查看状态并继续执行业务逻辑。

## express-session

安装：`npm install express-session`

### 主要方法：session(options)

作用：通过options指定参数来创建session中间件，仅仅只有session ID保存在cookie中，session数据保存在服务器中。<br>
options可选参数：

1. `name`：cookie中，保存session的字段名称（默认`connect.sid`）
2. `store`:session的**存储方式**，默认存放在内存中；也可以使用redis，mongodb等；
3. `secret`：通过设置的secret字符串，来计算hash值，并存放在cookie中，session cookie签名，**防篡改**；
4. `cookie`：设置存放session ID的cookie相关选项（默认：`{ path: ‘/’, httpOnly: true, secure: false, maxAge: null }`）
5. `genid`: 产生一个新的 session_id 时，所使用的函数（默认使用 uid2 这个 npm 包）；
6. `rolling`: 每个请求都重新设置一个 cookie（默认：false）
7. `resave`: 强制保存session即使它并没有变化（默认：true）
8. `proxy`：当设置了secure cookies（通过”x-forwarded-proto” header ）时信任反向代理。当设定为true时，”x-forwarded-proto” header 将被使用。当设定为false时，所有headers将被忽略。当该属性没有被设定时，将使用Express的trust proxy。
9. `saveUninitialized`：强制将未初始化的session存储。当新建了一个session且未设定属性或值时，它就处于未初始化状态。在设定一个cookie前，这对于登陆验证，减轻服务端存储压力，权限控制是有帮助的。（默认：true）
10. `unset`：控制req.session是否取消（例如通过 delete，或者将它的值设置为null）。这可以使session保持存储状态但忽略修改或删除的请求（默认：keep）

### express-session的一些方法

1. `Session.destroy()`:删除session，当检测到客户端关闭时调用。
2. `Session.reload()`:当session有修改时，刷新session。
3. `Session.regenerate()`：将已有session初始化。
4. `Session.save()`：保存session。

### cookie相关属性

- `Path`：表示 cookie 影响到的路，如 path=/。如果路径不能匹配时，浏览器则不发送这个Cookie；
- `httpOnly`：是微软对COOKIE做的扩展。如果在COOKIE中设置了“httpOnly”属性，则通过程序（JS脚本、applet等）将无法读取到COOKIE信息，防止XSS攻击产生；
- `secure`：当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效；
- `maxAge`：最大失效时间（毫秒），设置在多少后失效；


### express-session实例

	var express = require('express');
	var session = require('express-session');
	var app = express();
	
	// 使用session中间件
	// 只需要用use方法将session挂载在‘/’路径即可，这样所有的路由都可以访问到session。
	app.use(session({ 
	  secret: 'keyboard cat', //建议随机产生
	  cookie: ('name', 'value', { path: '/', httpOnly: true,secure: false, maxAge:  60000 }),
	  resave: true, //重新保存：强制会话保存即使是未修改的。默认为true但是得写上
	  saveUninitialized: true,//强制“未初始化”的会话保存到存储。
	}))
	
	app.get('/', function(req, res, next) {
	  var sess = req.session//用这个属性获取session中保存的数据，而且返回的JSON数据
	  if (sess.views) {
	    sess.views++
	    res.setHeader('Content-Type', 'text/html')
	    res.write('<p>欢迎第' + sess.views + '次访问' + 'expires in:' + (sess.cookie.maxAge/1000) + 's</p>')
	    res.end();
	  } else {
	    sess.views = 1
	    res.end('welcome to the session demo. refresh!')
	  }
	});
	app.listen(3000);