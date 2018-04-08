---
layout: post
title: "JavaScript全栈学习笔记（入门）"
date: 2018-03-11
description: "阮一峰全栈学习教程笔记"
tag: Node
---   

参考：[阮一峰：JavaScript 全栈工程师培训教程](http://www.ruanyifeng.com/blog/2016/11/javascript.html)<br>&emsp;&emsp;&emsp;[课堂练习的操作指导](https://github.com/ruanyf/jstraining/blob/master/demos/README.md)

# 目录
(目录并不完整，这里只是挑重点放上目录，以便整体把握)

- [一、环境搭建](#一环境搭建)
- [二、前端发展史](#二前端发展史)
	- [MVVM模式](#mvvm模式)
		- [SPA](#1spasingle-page-application单页应用)
		- [Angular](#2angular)
		- [Vue](#3vue)
	- [前后端分离](#前后端分离)
		- [REST接口](#rest接口)
		- [Node](#node)
- [三、React技术栈](#三react技术栈)
	- [JSX语法](jsx语法)
	- [Babel 转码器](#babel-转码器)
	- [React组件](#react组件)
		- [React组件语法](#react组件语法)
		- [React组件的参数](#react组件的参数)
		- [React 组件的状态](#react-组件的状态)
		- [React 组件库](#react-组件库)
	- [React架构—Flux架构](#react架构flux架构)
	- [React tips](#react-tips)
- [四、Node应用开发](#四node应用开发)
	- [一个简单的Node应用](#一个简单的node应用)
	- [REST API](#rest-api)
	- [Express 搭建 Web 应用](#express-搭建-web-应用)
- [五、前端工程](#五前端工程)

## 一、环境搭建

1. 安装Git
2. 安装Node：
	- 到官网[Nodejs](https://nodejs.org/en/)或者国内镜像<https://npm.taobao.org/mirrors/node>，下载安装包。
	- `$ node -v`：查看安装是否成功；
	- `npm`：node的模块管理器；
	- `$ npm config get registry`：查看源；
	- 由于Node的官方模块仓库网速太慢，模块仓库需要切换到阿里的源：<br>`$ npm config set registry https://registry.npm.taobao.org/`
3. 安装Postman<br>Postman是一种网页调试和发送网页http请求的Chrome浏览器插件。<br>
参考：<http://www.cnblogs.com/mafly/p/postman.html>



## 二、前端发展史
历史演变：前后端不分 -> 前后端分离 -> 全栈工程师

### 前后端不分的时代
1. 浏览器发出请求，后端收到浏览器请求；
2. 生成静态页面，发送给浏览器。

### 后端 MVC 的开发模式
- Model（模型层）：提供/保存数据
- Controller（控制层）：数据处理，实现业务逻辑
- View（视图层）：展示数据，提供用户界面

### web2.0
- `Ajax（异步 JavaScript 和 XML）`：是一种创建快速动态网页的技术，无需刷新网页就能够更新部分网页，通过在后台与服务器进行**少量**数据交换，使网页实现异步更新。
- 由于Ajax技术的出现，促成了web2.0的诞生。

### 前端MVC框架
&emsp;&emsp;前端通过Ajax得到数据，同样有了保存数据(M)、处理数据(C)、生成视图(V)的需求，这导致前端MVC诞生。
- `Backbone.js`：将前端分成两个部分
	- Model：管理数据
	- View：数据的展现
	- Controller：前端controller不应有业务逻辑，只需要处理UI逻辑，所以BackBone没有C，只用事件处理UI逻辑。
- `Router`：<br>作用：通过URL切换视图，例如：<br>![](/images/posts/180311/backbone-routing.png)

### MVVM模式
- Modle
- View
- View-Model：简化的Controller，唯一作用就是为View提供处理好的数据，不含其他逻辑。<br>**本质**：view 绑定 view-model，视图与数据模型强耦合。数据的变化实时反映在 view 上，不需要手动处理。

#### 1、SPA(Single-page application)单页应用
- 读写数据
- 切换视图
- 用户交互<br>传统架构：<br>![](/images/posts/180311/architecture-old.png)<br>单页应用架构：![](/images/posts/180311/architecture-new.png)

#### 2、Angular

- Google公司推出的Angular是最流行的MVVM前端框架。
- 它的风格属于HTML语言的增强，核心概念是**双向绑定**。

Angular的双向绑定：

	<div ng-app="">
	  <p>
	    姓名:<input type="text" ng-model="name" placeholder="在这里输入您的大名"/>
	  </p>
	  <h1>你好，{ {name} }</h1>
	</div>

ng-modle与name绑定，`View-Model`中，modle为view提供数据。

#### 3、Vue
- Vue.js是现在很热门的一种前端MVVM框架。
- 它的基本思想与Angular类似，但是用法更简单，而且引入了**响应式编程**的概念。

Vue的双向绑定：

	HTML代码：
	<div id="journal">
		 <input type="text" v-model="message">
		 <div>{ {message} }</div>
	</div>
	JS代码：
	var journal = new Vue({
	  el: '#journal',
	  data: {
	    message: 'Your first entry'
	  }
	});


v-modle与message绑定。

### 前后端分离
- Ajax -> 前端应用兴起
- 智能手机 -> 多终端支持

#### REST接口
`REST`即表述性状态传递(Representational State Transfer)<br>它是一种针对网络应用的设计和开发方式，可以降低开发的复杂性，提高系统的可伸缩性。<br>是一组架构约束条件和原则，满足这些约束条件和原则的应用程序或设计就是RESTful。

- 前后端分离以后，它们之间通过接口通信。
- 后端暴露出接口，前端消费后端提供的数据。
- 后端接口一般是`REST`形式，前后端的通信协议一般是`HTTP`。

#### Node
它是服务器上的 JavaScript 运行环境。<br>**Node = JavaScript + 操作系统API**

**Node的意义**：

- `JavaScript`成为服务器脚本语言与`Python`和`Ruby`一样
- `JavaScript`成为唯一的浏览器和服务器都支持的语言
- 前端工程师可以编写后端程序了

#### 前端开发模式的根本改变
- `Node`环境下开发
- 大量使用服务器端工具
- 引入**持续集成**等软件工程的标准流程<br>持续集成、持续交付、持续部署：
	- **集成**：是指软件个人研发的部分向软件整体部分交付，以便尽早发现个人开发部分的问题；
	- **部署**：是代码尽快向可运行的开发/测试节交付，以便尽早测试；
	- **交付**：是指研发尽快向客户交付，以便尽早发现生产环境中存在的问题。
- 开发完成后，编译成浏览器可以运行的脚本，放上[CDN](https://www.zhihu.com/question/37353035)(Content Delivery Network)即内容分发网络。

### 全栈
- 全栈工程师：
	- 一个人负责开发前端和后端
	- 从数据库到UI的所有开发
- 全栈技能：
	- 传统前端技能：HTML、JavaScript、CSS
	- 一门后端语言
	- 移动端开发：iOS / Android / HTML5
	- 其他技能：数据库、HTTP 等等

## 三、React技术栈
- React 是目前最热门的前端框架。
- React 是一个用于构建用户界面的JAVASCRIPT库。
- React 起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。
- 现在最好的社区支持和生态圈
- 大量的第三方工具

React 的优点：

- 组件模式：代码复用和团队分工
- 虚拟DOM：性能优势
- 移动端支持：跨终端

React 的缺点：React非常先进和强大，但是学习和实现成本都不低。

### JSX语法
React 使用 JSX 语法，JavaScript 代码中可以写 HTML 代码。

	let myTitle = <h1>Hello, world!</h1>;

- JSX 语法的最外层，只能有一个节点。
- JSX 语法中可以插入 JavaScript 代码，使用大括号。

```
let myTitle = <p>{'Hello ' + 'World'}</p>
```

### Babel 转码器
JavaScript 引擎（包括浏览器和 Node）都不认识 JSX，需要首先使用 Babel 转码，然后才能运行。

	<script src="react.js"></script>
	<script src="react-dom.js"></script>
	//React需要加载两个库，前者是 React 的核心库，后者是 React 的 DOM 适配库。
	<script src="babel.min.js"></script>
	//Babel 用来在浏览器转换 JSX 语法，如果服务器已经转好了，浏览器就不需要加载这个库。
	<script type="text/babel">
	  // ** Our code goes here! **
	</script>

示例：

	 <head>
	    <meta charset="utf-8">
	    <script src="react.js"></script>
	    <script src="react-dom.js"></script>
	    <script src="babel.min.js"></script>
	 </head>
	 <body>
	    <div id="example"></div>
	    <script type="text/babel">
			ReactDOM.render(
	  		<span>Hello World!</span>,
	  		document.getElementById('example')
			);
	    </script>
	 </body>

`ReactDOM.render`方法接受两个参数：一个虚拟 DOM 节点和一个真实 DOM 节点，作用是将虚拟 DOM 挂载到真实 DOM。

### React组件
React 允许用户定义自己的组件，插入网页。

#### React组件语法

	class MyTitle extends React.Component {
	  render() {
	    return <h1>Hello World</h1>;
	  }
	};

	ReactDOM.render(
	  <MyTitle/>,
	  document.getElementById('example')
	);

- `class MyTitle extends React.Component`： ES6 语法，表示自定义一个**MyTitle**类，该类继承了基类**React.Component**的所有属性和方法。
- React 规定，自定义组件的第一个字母必须大写，以便与内置的原生类相区分。
- 每个组件都必须由render方法，定义输出的样式。
- `<MyTitle/>`表示生成一个组件类的实例，每个实例一定要有闭合标签，写成`<MyTilte></MyTitle>`也可。

#### React组件的参数
组件内部通过`this.props`对象获取参数：

	<body>
	<div id="example"></div>
	<script type="text/babel">
	  class MyTitle extends React.Component {
	    render() {
	      return <h1 style= { {color: this.props.color} }>Hello World</h1>;
	    }
	  };

	  ReactDOM.render(
	    <MyTitle color="red" />,
	    document.getElementById('example')
	  );
	</script>
	</body>


#### React 组件的状态

	<body>
	<div id="example"></div>
	<script type="text/babel">
	  class MyTitle extends React.Component {
	    constructor(...args) {
	      super(...args);
	      this.state = {
	        name: '访问者'
	      };
	    }

	    handleChange(e) {
	      let name = e.target.value;
	      this.setState({
	        name: name
	      });
	    }

	    render() {
	      return <div>
	        <input type="text" onChange={this.handleChange.bind(this)} />
	        <p>你好，{this.state.name}</p>
	      </div>;
	    }
	  };

	  ReactDOM.render(
	    <MyTitle/>,
	    document.getElementById('example')
	  );
	</script>
	</body>


- `constructor`是组件的构造函数，会在创建实例时自动调用。<br>`...args`表示组件参数，`super(...args)`是 ES6 规定的写法。<br>`this.state对象`用来存放内部状态，这里是定义初始状态。
- 组件内部状态：用`this.state`对象表示
- 当input元素发生onChange事件时，调用onChange事件指定的监听函数`this.handleChange`(this表示当前组件)<br>`.bind(this)` 表示：`this.handleChange`方法内部的this，绑定当前组件。
- `this.setState`方法用来重置this.state，每次调用这个方法，就会引发组件的重新渲染。

#### React 组件的生命周期
React 为组件的不同生命阶段，提供了七个**钩子方法**：

- componentWillMount：组件渲染前被调用
- **componentDidMount**：组件第一次渲染后调用，只执行一次
- componentWillUpdate：组件更新前被调用（收到新的props或者state但还没有render时）
- componentDidUpdate：组件更新后调用
- componentWillUnmount：组件从DOM中移除的时调用。
- componentWillReceiveProps：组件接受新的参数时调用
- shouldComponentUpdate

#### React 组件库
React 的一大优势，就是网上有很多已经写好的组件库，可以使用。<br>
`React-Bootstrap`：<https://react-bootstrap.github.io/><br>
`ReCharts`：是一个 React 图表组件库。<http://recharts.org/><br>
如何使用第三方组件库:

	<head>
	    <meta charset="utf-8">
	    <script src="react-with-addons.min.js"></script>
	    <script src="react-dom.js"></script>
	    <script src="react-dom-server.min.js"></script>
	    <script src="Recharts.min.js"></script>
	    <script src="babel.min.js"></script>
	</head>
	<body>
	    <div id="example" style="width: 1000px;height: 800px;"></div>
	    <script type="text/babel">
			const {LineChart, Line, XAxis, YAxis, CartesianGrid} = Recharts;
			const data = [
			      {name: 'Page A', uv: 4000, pv: 2400, amt: 2400},
			      {name: 'Page B', uv: 3000, pv: 1398, amt: 2210},
			      {name: 'Page C', uv: 2000, pv: 9800, amt: 2290},
			      {name: 'Page D', uv: 2780, pv: 3908, amt: 2000},
			      {name: 'Page E', uv: 1890, pv: 4800, amt: 2181},
			      {name: 'Page F', uv: 2390, pv: 3800, amt: 2500},
			      {name: 'Page G', uv: 3490, pv: 4300, amt: 2100},
			];

			const TinyLineChart = React.createClass({
				render () {
			  	return (
			  <LineChart width={1000} height={400} data={data}>
			    <XAxis dataKey="name"/>
			    <YAxis/>
			    <CartesianGrid stroke="#eee" strokeDasharray="5 5"/>
			    <Line type="monotone" dataKey="uv" stroke="#8884d8" />
			    <Line type="monotone" dataKey="pv" stroke="#82ca9d" />
			  </LineChart>
			    );
			  }
			})

			ReactDOM.render(
			  <TinyLineChart />,
			  document.getElementById('example')
			);
	    </script>
	</body>
创建第三方组件用函数：`React.createClass`

### React架构---Flux架构
Facebook 提出`Flux`架构的概念，被认为是`React`应用的标准架构。
![](/images/posts/180311/flow.png)
最大特点：数据单向流动。与 MVVM 的数据双向绑定，形成鲜明对比。

核心思想：

- 不同组件的state，存放在一个外部的、公共的 Store 上面。、
- 组件订阅 Store 的不同部分。
- 组件发送（dispatch）动作（action），引发 Store 的更新。

Flux 只是一个概念，有30多种实现。

#### 流行的两个React架构
React 架构的最重要作用：管理 Store 与 View 之间的关系。

- `MobX`：响应式（Reactive）管理，state 是可变对象，适合中小型项目
- `Redux`：函数式（Functional）管理，state 是不可变对象，适合大型项目

(目前还未去了解这两种方式的架构，有待学习)

### React tips

- JSX语法：JS中可以插入HTML，而插入的HTML中又可以插入JS（用大括号括起来）。
- React：用JSX语法，自定义组件或者引用第三方组件（虚拟 DOM 节点：代码复用），将其挂载到真实DOM节点`ReactDOM.render`到页面。
- **React核心思想**：View是State的输出；*view = f(state)，其中f表示函数关系*<br>**React其本质**：是将图像界面（GUI）函数化
- $.getJSON()

使用`AJAX`的`HTTP GET`请求获取`JSON`数据。

	$(selector).getJSON(url,data,success(data,status,xhr))

- .forEach()

例：

	items.forEach(item=>{
		var name=item.name;
		……
	});
	或者：
	items.forEach(function(item){
		var name=item.name;
		……
	});

## 四、Node应用开发

- `Node`：服务器的 JavaScript 运行环境，提供 API 与操作系统互动。
- `npm`：Node 的模块管理器，开发 Node 项目的必备工具。
- Node 开发前端脚本的好:
	- 模块机制
	- 版本管理
	- 对外发布
	- [持续集成](#node)的标准开发流程
- npm 配置文件：`package.json` -->[详情](https://docs.npmjs.com/files/package.json)
- 路由：是指如何定义应用的端点（URIs）以及如何响应客户端的请求<br>
结构：`app.METHOD(path, [callback...], callback)`
	- app 是 express 对象的一个实例；
	- METHOD 是一个 HTTP 请求方法；
	- path 是**服务器上的路径**；
	- callback 是当路由匹配时要执行的函数。


### node有关命令

- 安装 Node 模块时，如果指定了 --save 参数，那么此模块将被添加到 package.json 文件中 dependencies 依赖列表中。 然后通过 npm install 命令即可自动安装依赖列表中所列出的所有模块。

### 一个简单的Node应用
`webPack`：可以看做是`模块打包机`：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），并将其转换和打包为合适的格式供浏览器使用。

1、新建一个目录：<br>
&emsp;&emsp;`mkdir simple-app-demo`<br>
&emsp;&emsp;`cd simple-app-demo`

2、创建项目的配置文件：`package.json`<br>
&emsp;&emsp;`npm init -y`

3、安装需要的模块：`jquery`和`webpack`这两个模块<br>
&emsp;&emsp;`npm install -S jquery`<br>
&emsp;&emsp;`npm install -S webpack`<br>
&emsp;&emsp;打开`package.json`文件，会发现`jquery`和`webpack`都加入了`dependencies`字段，并且带有版本号。

4、 在项目根目录下，新建一个网页文件：`index.html`：

	<html>
	  <body>
	    <h1>Hello World</h1>
	    <script src="bundle.js"></script>
	  </body>
	</html>

5、 在项目根目录下，新建一个脚本文件app.js

	const $ = require('jquery');
	$('h1').css({ color: 'red'});

6、打开package.json，在scripts字段里面，添加`build`一行。

	  "scripts": {
	    "build": "webpack app.js --output-filename bundle.js  --output-path . --mode development",
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },

7、在项目根目录下，执行将脚本打包的命令：<br>
&emsp;&emsp;`npm run build`<br>
&emsp;&emsp;执行完成，可以发现项目根目录下，新生成了一个文件bundle.js。<br>
&emsp;&emsp;Error：[打包时遇到的错误](/2018/03/Node-error)

8、浏览器打开index.html，可以发现Hello World变成了红色。

9、关于Node的简单应用实现。

### REST API
[REST](#rest接口)是浏览器与服务器通信方式的一种`设计风格`。

`REpresentational State Transfer`：

- Resource：资源
- Representation：表现层
- State：状态
- Transfer：转换
<hr>
REST 的核心概念:

1. 互联网上所有可以访问的内容，都是资源。
2. 服务器保存资源，客户端请求资源。
3. 同一个资源，有多种表现形式。
4. 协议本身不带有状态，通信时客户端必须通过参数，表示请求不同状态的资源。
5. 状态转换通过HTTP动词表示。
<hr>
`URL`：是资源的唯一识别符。
<hr>
`查询字符串` （get请求）：表示对所请求资源的约束条件-->`GET/zoos/1/animals?limit=10&offset=10`
<hr>
**HTTP动词**：

|操作	|SQL方法	|HTTP动词|
|-------|-------|--------|
|CREATE(新建)	|INSERT	|POST|
|READ(查询)	|SELECT	|GET|
|UPDATE(修改)	|UPDATE	|PUT/PATCH|
|DELETE(删除)	|DELETE	|DELETE|

- GET /v1/stores/1234
- PUT /v1/stores/1234
- POST /v1/stores
- DELETE /v1/stores/1234
<hr>
#### REST API demo
**json-server快速“伪造”后台接口**

1、 `mkdir rest-api-demo`<br>
&emsp;&emsp;`cd rest-api-demo`<br>
&emsp;&emsp;`npm init -y`

2、 安装模块<br>
&emsp;&emsp;`npm install -S json-server`

3、在项目根目录下，新建一个 JSON 文件`db.json`

	{
	  "posts": [
	    { "id": 1, "title": "json-server", "author": "typicode" }
	  ],
	  "comments": [
	    { "id": 1, "body": "some comment", "postId": 1 }
	  ],
	  "profile": { "name": "typicode" }
	}


4、 打开`package.json`，在scripts字段添加一行。（`db.json`数据存到服务器）

	"scripts": {
	  "server": "json-server db.json",
	  "test": "..."
	},

5、 启动服务器：<br>
&emsp;&emsp;`npm run server`
![](/images/posts/180311/server.png)
三个接口已经生成：

- posts
- comments
- profile
- 支持post(新增) delete(删除) put(修改) get(查询);

6、打开`Postman`：<br>
依次向`http://127.0.0.1:3000/posts`、`http://127.0.0.1:3000/posts/1`发出`GET`请求
![](/images/posts/180311/get1.png)![](/images/posts/180311/get2.png)
**注意**：第一个`GET`请求得到的是key=>posts里的全部items；第二个`GET`请求得到的是`id=1`的那个item。

7、向`http://127.0.0.1:3000/comments`发出`POST`请求。<br>
注意，数据体Body要选择`x-www-form-urlencoded`编码，然后依次添加下面两个字段：

	body: "hello world"
	postId: 1
![](/images/posts/180311/post1.png)
`添加`item到comments，`Body`中为要添加的内容，其中自动生成id。
![](/images/posts/180311/get3.png)

8、向`http://127.0.0.1:3000/comments/2`发出`PUT`请求。<br>
数据体Body选择`x-www-form-urlencoded`编码，然后添加下面字段：

	body: "hello react"
![](/images/posts/180311/put1.png)
`修改`comments中`id=2`的item
![](/images/posts/180311/get4.png)

9、向`http://127.0.0.1:3000/comments/2`发出`delete`请求
![](/images/posts/180311/delete1.png)
`删除`comments中`id=2`的item
![](/images/posts/180311/get5.png)

10、向`http://127.0.0.1:3000/db`发送`GET`请求，得到的就是整个`db.json`里的数据。

11、`ctl+C` 终止server。

#### 总结：

- Node中`json-server`包：
	- 主要作用是：搭建一台JSON服务器，测试一些业务逻辑


### Express 搭建 Web 应用

- `Express`：是最常用的Node框架，用来搭建`Web`应用，有丰富的`HTTP`工具；<br>
- `Express`不对 node.js 已有的特性进行二次抽象，只是在它之上扩展了Web应用所需的功能。
- `Express`框架核心特性：
	- 可以设置`中间件`来响应 HTTP 请求；
	- 定义了`路由`表用于执行不同的 HTTP 请求动作；
	- 可以通过向模板传递参数来动态渲染 HTML 页面。
- 整个`Express`的设计哲学就是利用`中间件`，不断对`HTTP`请求加工，然后返回一个`HTTP`响应。
- 定义一个路由
- 中间件：对HTTP请求进行加工


1、`npm install`安装依赖

2、app1.js<br>
1) 调用`express`模块，创建一个`web实例` --> app

	var express    = require('express');
	var app        = express();

2) 新建了一个路由对象，该对象指定访问服务器根目录（/）时，服务器响应返回：`<h1>Hello World</h1>`。将路由加载至`/home`路径，即访问`/home`返回`Hello World`。

	var router = express.Router();

	router.get('/', function(req, res) {
	  res.send('<h1>Hello World</h1>');
	});

	app.use('/home', router);

- router.get()方法：

	- 第一个参数：服务器上的路径
	- 第二个参数：路由匹配时要执行的`回调函数`：
		- req和res：Express 内置的对象；
		- req：用户的请求；
		- res：web服务器的响应。
- res.send()方法：服务器响应是送出的内容。

3) 第一行指定外部访问的端口：要么通过环境变量指定，或者环境变量没有指定则默认8080端口。<br>
后两行是启动应用，监听指定端口，并在控制台打印一行文字。

	var port = process.env.PORT || 8080;

	app.listen(port);
	console.log('Magic happens on port ' + port);

![](/images/posts/180311/express-app1.png)

4) 通过浏览器访问：`localhost:8080/home`，输出`Hello World`。

5) 通过环境变量，自定义启动端口。<br>
假定我们指定必须启动在7070端口，命令行可以这样操作：

	# Linux & Mac
	$ PORT=7070 node app1.js

	# windows
	$ set PORT=7070
	$ node app1.js
浏览器就可以访问`localhost:7070/home`了。

3、app2.js<br>
新增路由，这个路由的路径是一个命名参数:`name`，可以从`req.params.name`拿到这个传入的参数。

	router.get('/:name', function(req, res) {
	  res.send('<h1>Hello ' + req.params.name + '</h1>');
	});

`node app2.js` 启动这个应用。

浏览器访问`localhost:8080/home/xuxu`，输出Hello xuxu。

![](/images/posts/180311/express-app2.png)

4、app3.js<br>
1) `body-parser`模块的作用：对POST、PUT、DELETE等 HTTP 方法的数据体进行解析；<br>
`app.use`：用来将这个模块加载到当前应用；<br>
有了这两句，就可以处理POST、PUT、DELETE等请求了。

	var express    = require('express');
	var app        = express();

	var bodyParser = require('body-parser');
	app.use(bodyParser.urlencoded({ extended: true }));

2) 新增路由：如果收到了`/`路径（实际上是/home路径）的`POST`请求，先从数据体拿到`name`字段，然后返回一段`JSON`信息。

	router.post('/', function (req, res) {
	  var name = req.body.name;
	  res.json({message: 'Hello ' + name});
	});

`node app3.js` 启动这个应用。

在`Postman`中，向`http://127.0.0.1:8080/home`发出一个`POST`请求.<br>
数据体的编码方法设为`x-www-form-urlencoded`，里面设置一个name字段.

	POST /home HTTP/1.1
	Host: 127.0.0.1:8080
	Content-Type: application/x-www-form-urlencoded

	name=xxuux

服务器返回一段JSON信息。
![](/images/posts/180311/express-app3.png)

4、app4.js<br>
1）`router.use`的作用是加载一个函数，这个函数被称为`中间件`：<br>
&emsp;&emsp;作用是：在请求被路由匹配之前，做一些处理。<br>
&emsp;&emsp;next()：代表下一个中间件，表示将处理过的请求传递给下一个中间件。

	router.use(function(req, res, next) {
	  console.log('There is a requesting.');
	  next();
	});

2）添加中间件，打印日期：

	router.use(function(req, res, next) {
	  var date=new Date();
	  var year=date.getFullYear();
	  var month=date.getMonth()+1;
	  var day=date.getDate()
	  var str=year+"-"+month+"-"+day;
	  console.log(str);
	  next();
	});


3）get传参：浏览器通过`http://127.0.0.1:8080/home?name=xx`访问，`req.query.name`获取参数的值：

	router.get('/', function(req, res) {
	  res.send('<h1>Hello '+req.query.name+'</h1>');
	});


4）占位符传参：浏览器必须严格按照`http://127.0.0.1:8080/home/xxx/yyy`的形式访问，通过`req.params.name`获取对应的参数的值:

	router.get('/:id/:name', function(req, res, next) {
	  res.send('<h1>Hello '+req.params.name+'</h1>');
	});

## 五、前端工程
1、`持续集成`，Continuous integration（简称 CI）：开发代码频繁地合并进主干，始终保持可发布状态的这个过程。

流程：

- 本地开发（developing）
- 静态代码检查（linting）
- 单元测试（testing）
- 合并进入主干（merging）
- 自动构建（building）
- 自动发布（publishing）

优点：

- 快速发现错误
- 防止分支大幅偏离主干
- 让产品可以快速迭代，同时还能保持高质量

2、`测试`：Web 应用越来越复杂，意味着更可能出错。测试是提高代码质量、降低错误的最好方法之一。

测试的类型：

- 单元测试（unit testing）
	- Mocha
	- 单元测试是用来对一个模块、一个函数或者一个类来进行正确性检验的测试工作。
- 功能测试（feature testing）
	- 功能测试必须在真正浏览器做，现在有四种方法:
		- 使用本机安装的浏览器
		- 使用 Selenium Driver
		- 使用 Headless Chrome
		- 使用 Electron
	- 站在外部用户的角度，测试软件的某项功能。与内部代码实现无关，只测试功能是否正常。很多时候，单元测试都可以通过，但是整体功能会失败。
- 集成测试（integration testing）
	- 持续集成服务平台：代码合并进主干以后，就可以进行自动构建和发布了。
	- 网上有很多 PaaS 平台，提供持续集成服务。
	- Travis CI 就是其中最著名的一个，它可以根据你提供的脚本，自动完成构建和发布。
- 端对端测试 (End-to-End testing）

以测试为导向的开发模式：

- TDD：测试驱动的开发（Test-Driven Development）
- BDD：行为驱动的开发（Behavior-Driven Development）
- TDD：基于开发者角度，重点测试函数的输入输出
- BDD：基于使用者角度，重点测试对用户行为的反应

### ESLint

- `ESLint`：静态代码检查工具
- 发现语法错误
- 发现风格错误
- 自动纠正错误

### Mocha

- `Mocha`目前最常用的测试框架。
- mocha是JavaScript的一种单元测试框架，既可以在浏览器环境下运行，也可以在Node.js环境下运行。


### Nightmare

- `Nightmare`：使用 Electron 模拟真实浏览器环境，功能测试。

### Travis CI

- 持续集成
