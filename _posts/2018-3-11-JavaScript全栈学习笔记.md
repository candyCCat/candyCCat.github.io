---
layout: post
title: "JavaScript全栈学习笔记（入门）"
date: 2018-03-11
description: "阮一峰全栈学习教程笔记"
tag: JS全栈
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
- [](#)
- [](#)

## 一、环境搭建

1. 安装Git
2. 安装Node：
	- 到官网[Nodejs](https://nodejs.org/en/)或者国内镜像<https://npm.taobao.org/mirrors/node>，下载安装包。
	- `$ node -v`：查看安装是否成功；
	- `npm`：node的模块管理器；
	- `$ npm config get registry`：查看源；
	- 由于Node的官方模块仓库网速太慢，模块仓库需要切换到阿里的源：<br>`$ npm config set registry https://registry.npm.taobao.org/`
3. 安装Postman<br>Postman是一种网页调试和发送网页http请求的Chrome浏览器插件。

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

```
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
```
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

### 一个简单的Node应用
[dianjie](/2018/03/React/)