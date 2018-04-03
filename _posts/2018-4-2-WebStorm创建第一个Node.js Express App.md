---
layout: post
title: "WebStorm创建第一个Node.js Express App"
date: 2018-04-2
description: "利用express-generator创建express项目"
tag: node
---   


- 前提：安装`node`和`npm`包管理工具；
- `npm install express-generator -g`：`-g`全局安装express应用的目录生成工具；

### 出现问题：

![](/images/posts/180402/create-expressPro-error.png)

- 原因： 4.X 版本 express.js 文件名称改变；
- 解决方法：
	- 1. 使用命令行方式创建项目，再用`WebStorm`打开。
	- 2. 构建项目时，`Version`选择 4.14.1 版本或以下（必须下载大于等于该版本的`express-generator`）。

### cmd创建项目

1）进入想要创建项目的目录

2）创建一个模板引擎为 ejs，应用名叫 testNode 的工程：

	express --view=ejs testNode

输出如下：

	   create : testNode\
	   create : testNode\public\
	   create : testNode\public\javascripts\
	   create : testNode\public\images\
	   create : testNode\public\stylesheets\
	   create : testNode\public\stylesheets\style.css
	   create : testNode\routes\
	   create : testNode\routes\index.js
	   create : testNode\routes\users.js
	   create : testNode\views\
	   create : testNode\views\error.ejs
	   create : testNode\views\index.ejs
	   create : testNode\app.js
	   create : testNode\package.json
	   create : testNode\bin\
	   create : testNode\bin\www

	   change directory:
	     > cd testNode

	   install dependencies:
	     > npm install

	   run the app:
	     > SET DEBUG=testnode:* & npm start

3）按照提示：`cd testNode`、`npm install`-->进入项目目录，安装依赖包；

4）生成目录：(已经生成一个可运行的Demo)<br>
![](/images/posts/180402/content.png)

- bin：是真实的执行程序
- node_modules：存放所有的项目依赖库
- public：静态文件(css,js,img)
- routes：路由文件
- views：页面文件
- app.js：程序启动文件
- package.json：项目依赖配置及开发者信息

### 启动服务器

方法一：`npm start`<br>
在浏览器中打开`http://localhost:3000`运行成功。

方法二：在WebStorm中，点击`编辑结构`-->`添加新配置`-->`点击绿色按钮运行`<br>
![](/images/posts/180402/create-expressPro-step.png)![](/images/posts/180402/create-expressPro-step1.png)
