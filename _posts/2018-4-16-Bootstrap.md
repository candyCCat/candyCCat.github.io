---
layout: post
title: "Bootstrap 4"
date: 2018-04-16
description: ""
tag: Node
---  

## 目录

- [网格类](#网格类)
- [文字排版](#文字排版)
- [文本颜色、背景颜色类](#文本颜色背景颜色类)
- [table表格](#表格)
- [img图像相关类](#图像相关类)
- [Jumbotron](#jumbotron)
- [alert信息提示框](#alert信息提示框)
- [btn按钮](#btn按钮)
- [btn-group按钮](#btn-group按钮)
- [badge徽章类](#badge徽章类)
- [progress进度条类](#progress进度条类)
- [分页](#分页)
- [面包屑导航](#面包屑导航)
- [list-group列表组](#list-group列表组)
- [卡片](#卡片)
- [下拉菜单](#下拉菜单)
- [折叠](#折叠)
- [导航](#导航)
- [导航条](#导航条)
- [表单](#表单)
- [应用实例](#应用实例)
- [小小工具](#小小工具)




### 使用实例1：

	<!DOCTYPE html>
	<html>
	<head>
	  <title>Bootstrap 实例</title>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1">

	  <!-- 新 Bootstrap4 核心 CSS 文件 -->
	  <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0-beta/css/bootstrap.min.css">

	  <!-- jQuery文件。务必在bootstrap.min.js 之前引入 -->
	  <script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>

	  <!-- popper.min.js 用于弹窗、提示、下拉菜单 -->
	  <script src="https://cdn.bootcss.com/popper.js/1.12.5/umd/popper.min.js"></script>

      <!-- 最新的 Bootstrap4 核心 JavaScript 文件 -->
	  <script src="https://cdn.bootcss.com/bootstrap/4.0.0-beta/js/bootstrap.min.js"></script>

	</head>
	<body>

	<div class="jumbotron text-center">
	  <h1>我的第一个 Bootstrap 页面</h1>
	  <p>重置浏览器大小查看效果!</p>
	</div>

	<div class="container">
	  <div class="row">
	    <div class="col-sm-4">
	      <h3>第一列</h3>
	      <p>菜鸟教程</p>
	      <p>学的不仅是技术，更是梦想！！！</p>
	    </div>
	    <div class="col-sm-4">
	      <h3>第二列</h3>
	      <p>菜鸟教程..</p>
	      <p>学的不仅是技术，更是梦想！！！</p>
	    </div>
	    <div class="col-sm-4">
	      <h3>第三列</h3>
	      <p>菜鸟教程..</p>
	      <p>学的不仅是技术，更是梦想！！！</p>
	    </div>
	  </div>
	</div>

	</body>
	</html>


### 网格类

一共将屏幕分为12列：

- `.col-` ：针对所有设备
- `.col-sm-` ：平板，屏幕宽度等于或大于 576px
- `.col-md-` ：桌面显示器，屏幕宽度等于或大于 768px
- `.col-lg-` ：大桌面显示器，屏幕宽度等于或大于 992px
- `.col-xl-` ：超大桌面显示器，屏幕宽度等于或大于 1200px

自动处理布局（每一列等宽）：

	<div class="row">
	  <div class="col"></div>
	  <div class="col"></div>
	  <div class="col"></div>
	</div>

### 文字排版

Display标题类：`.display-1`, `.display-2`, `.display-3`, `.display-4`<br>
可改变`<h></h>`标签的大小。

***

`<small>`：用于创建字号更小的颜色更浅的文本；

***

`<mark>`：高亮文本，黄色背景及有一定的内边距；

***

`<abbr>`：文本下划线，鼠标hover显示title内容，例：<br>
`<abbr title="World Health Organization">WHO</abbr>`，效果：<br>
![](/images/posts/180416/bootstrap1.png)

***

`<blockquote>`：用于引用内容，例：<br>

```
<blockquote class="blockquote">
  <p>失败是成功之母。</p>
  <footer class="blockquote-footer">爱迪生</footer>
</blockquote>
```
![](/images/posts/180416/bootstrap2.png)

***

`dl-->dt-->dd`

***

`<code>`：代码段

***

`<kbd>`：键盘文本，效果：<br>
![](/images/posts/180416/bootstrap3.png)

***

`<pre>`：定义预格式化文本，被包围在标签中的文本保留空格换行符；

***

更多排版类：


|类名|作用|
|-|-|
|`.font-weight-bold`|加粗文本|
|`.font-weight-normal`|普通文本|
|`.font-weight-light`|更细的文本|
|`.font-italic`|斜体文本|
|——| |
|`.lead`|让段落更突出|
|`.small`|指定更小文本 (为父元素的 85% )|
|——| |
|`.text-left`|左对齐|
|`.text-center`|居中|
|`.text-right	`|右对齐|
|************||
|`.text-justify`|设定文本对齐,段落中超出屏幕部分文字自动换行|
|`.text-nowrap`|段落中超出屏幕部分不换行|
|************| |
|`.text-lowercase`|设定文本小写|
|`.text-uppercase`|设定文本大写|
|`.text-capitalize`|设定单词首字母大写|
|************| |
|`.initialism`|显示在 <abbr> 元素中的文本以小号字体展示，且可以将小写字母转换为大写字母
|—**列表样式：**—| |
|`.list-unstyled`|移除默认的列表样式，列表项中左对齐 ( `<ul>`和 `<ol>` 中)。<br>这个类仅适用于直接子列表项 (如果需要移除嵌套的列表项，你需要在嵌套的列表中使用该样式)|
|`.list-inline`|将所有列表项放置同一行|
|——| |
|`.pre-scrollable`|使 <pre> 元素可滚动，代码块区域最大高度为340px,一旦超出这个高度,就会在Y轴出现滚动条|

### 文本颜色、背景颜色类

|类名|作用|
|-|-|
|**文本颜色**：| |
|`.text-muted`|灰色|
|`.text-primary`|蓝色|
|`.text-success`|绿色|
|`.text-info`|浅蓝|
|`.text-warning`|黄色|
|`.text-danger`|红色|
|`.text-secondary`|灰色|
|`.text-dark`|深灰|
|`.text-light`|浅灰（白色背景看不清）|
|`.text-white`|白色|
|**背景颜色**：| |
|`.bg-primary`|蓝|
|`.bg-success`|绿|
|`.bg-info`|浅蓝|
|`.bg-warning`|黄|
|`.bg-danger`|红|
|`.bg-secondary`|灰|
|`.bg-dark`|深灰|
|`.bg-light`|浅灰|

### 表格

表格框架：

	<table class="table">
	    <thead>
	      <tr>
	        <th>Firstname</th>
	        <th>Lastname</th>
	        <th>Email</th>
	      </tr>
	    </thead>
	    <tbody>
	      <tr>
	        <td>John</td>
	        <td>Doe</td>
	        <td>john@example.com</td>
	      </tr>		
		…………
	    </tbody>
	</table>

***

- `.table-striped`：条纹表格<br>
`<table class="table table-striped">`
- `.table-bordered`：带边框表格<br>
`<table class="table table-bordered">`
- `.table-hover`：鼠标悬停状态表格<br>
`<table class="table table-hover">`
- `table-dark`：黑色背景表格<br>
`<table class="table table-dark">`
- `.table-sm`：用于减少表格内边距设置较小表格<br>
`<table class="table table-bordered table-sm">`
- `.table-responsive`：响应式表格：在屏幕宽度小于 992px 时会创建水平滚动条<br>

```
<div class="table-responsive">
<table class="table">
…………
</table>
</div>
```
指定屏幕宽度：

|类名|屏幕宽度|
|-|-|
|.table-responsive-sm	|< 576px|
|.table-responsive-md	|< 768px|
|.table-responsive-lg	|< 992px|
|.table-responsive-xl	|< 1200px|

***

表格颜色类，可指定行`<tr>`或者单元格`<td>`的颜色：

|类名|作用|
|-|-|
|`.table-primary`|蓝色|
|`.table-success`|绿色|
|`.table-danger`|红色|
|`.table-info`|浅蓝色|
|`.table-warning`|橘色|
|`.table-active`|灰色: 用于鼠标悬停效果|
|`.table-secondary`|灰色: 表示内容不怎么重要|
|`.table-light`|浅灰色，可以是表格行的背景|
|`.table-dark`|深灰色，可以是表格行的背景|

表头背景颜色：

|类名|作用|
|-|-|
|.thead-dark|黑色|
|.thead-light|灰色|
|.thead-inverse|黑色|
|.thead-default|灰色|

### <img>图像相关类

- `.rounded`：图片圆角
- `.rounded-circle`：椭圆
- `.img-thumbnail`：设置图片缩略图（图片边框）
- `.float-right`和`.float-left`：左右对齐
- `.img-fluid`：响应式

### Jumbotron

- `.jumbotron`：创建灰色背景大框（带圆角）
- `.jumbotron-fluid`：创建没有圆角的大框<br>
在 .jumbotron-fluid 类里头的 div添加 `.container `或 `.container-fluid`：

```
<div class="jumbotron jumbotron-fluid">
  <div class="container">
      <h1>菜鸟教程</h1>
      <p>学的不仅是技术，更是梦想！！！</p>
  </div>
</div>
```

### alert信息提示框

在`.alert`类后加上：

- `.alert-success`
- `.alert-info`
- `.alert-warning`
- `.alert-danger`
- `.alert-primary`
- `.alert-secondary`
- `.alert-light`
- `.alert-dark`

***

- `.alert-link`：提示框中添加链接<br>

``` html
<div class="alert alert-success">
  <strong>成功!</strong> 你应该认真阅读 <a href="#" class="alert-link">这条信息</a>。
</div>
```

***

- `.alert-dismissable`：在这个之后的关闭按钮添加`class="close" `和 `data-dismiss="alert" `类来设置提示框的关闭操作：

``` html
<div class="alert alert-success alert-dismissable">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <strong>成功!</strong> 指定操作成功提示信息。
</div>
```

**注：`&times;`(×) 是 HTML 实体字符，来表示关闭操作，而不是字母 "x"。**

### btn按钮

按钮类可用于`<a>`, `<button>`, 或 `<input>` 元素上:<br>
在`btn`之后添加：

- `.btn-primary`
- `.btn-success`
- `.btn-info`
- `.btn-warning`
- `.btn-danger`
- `.btn-secondary`
- `.btn-dark`
- `.btn-light`
- `.btn-link`

有边框的按钮：

- `.btn-outline-primary`
- `.btn-outline-success`
- `.btn-outline-info`
- `.btn-outline-warning`
- `.btn-outline-danger`
- `.btn-outline-secondary`
- `.btn-outline-dark`
- `.btn-outline-light`

设置按钮大小：

- `.btn-lg`
- `.btn-sm`

块级按钮：（占一行）

- `.btn-block`

激活和禁用：`.activ`、`disabled`：

	<button type="button" class="btn btn-primary active">点击后的按钮</button>
	<button type="button" class="btn btn-primary" disabled>禁止点击的按钮</button>
	<a href="#" class="btn btn-primary disabled">禁止点击的链接</a>

### btn-group按钮组

	<div class="btn-group">
	  <button type="button" class="btn btn-primary">Apple</button>
	  <button type="button" class="btn btn-primary">Samsung</button>
	  <button type="button" class="btn btn-primary">Sony</button>
	</div>

***

- `.btn-group-lg|sm|xs`：设置按钮的大小
- `.btn-group-vertical`：垂直按钮组

***

内嵌按钮组及下拉菜单实例：

	<div class="btn-group">
	  <button type="button" class="btn btn-primary">Apple</button>
	  <button type="button" class="btn btn-primary">Samsung</button>
	  <div class="btn-group">
	    <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Sony</button>
	    <div class="dropdown-menu">
	      <a class="dropdown-item" href="#">Tablet</a>
	      <a class="dropdown-item" href="#">Smartphone</a>
	    </div>
	  </div>
	</div>

### badge徽章类

在类.badge之后加上：

- `.badge-primary`
- `.badge-success`
- `.badge-danger`
- `.badge-warning`
- `.badge-info`
- `.badge-secondary`
- `.badge-light`
- `.badge-dark`
- `.badge-pill`：药丸形状

### progress进度条类

`progress`和`progress-bar`：

	<div class="progress">
	  <div class="progress-bar" style="width:70%"></div>
	</div>

- 进度条高度默认：16px，修改CSS`height`改变高度；
- 进度条颜色默认：蓝色，改变颜色改变背景颜色，或者添加：`bg-danger`类等；
- `.progress-bar-striped`：设置条纹进度条；
- `.progress-bar-striped`+`.progress-bar-animated`：动画进度条；

混合色彩进度条：

	<div class="progress">
	  <div class="progress-bar bg-success" style="width:40%">
	    Free Space
	  </div>
	  <div class="progress-bar bg-warning" style="width:10%">
	    Warning
	  </div>
	  <div class="progress-bar bg-danger" style="width:20%">
	    Danger
	  </div>
	</div>

### 分页

在`ul`上添加`.pagination`类，`li`标签上添加`.page-item`类：

	<ul class="pagination">
	  <li class="page-item"><a class="page-link" href="#">Previous</a></li>
	  <li class="page-item"><a class="page-link" href="#">1</a></li>
	  <li class="page-item"><a class="page-link" href="#">2</a></li>
	  <li class="page-item"><a class="page-link" href="#">3</a></li>
	  <li class="page-item"><a class="page-link" href="#">Next</a></li>
	</ul>

- `.active`：高亮显示当前页
- `.disabled`：分页连接不可点

设置分页条目大小：

- `.pagination-lg`
- `.pagination-sm`

### 面包屑导航

`.breadcrumb`和`.breadcrumb-item`类用于设置面包屑导航：

	<ul class="breadcrumb">
	  <li class="breadcrumb-item"><a href="#">Photos</a></li>
	  <li class="breadcrumb-item"><a href="#">Summer 2017</a></li>
	  <li class="breadcrumb-item"><a href="#">Italy</a></li>
	  <li class="breadcrumb-item active">Rome</li>
	</ul>

效果：<br>
![](/images/posts/180416/bootstrap4.png)

### list-group列表组

在`ul`上添加`.list-group `类，`li`标签上添加`.list-group-item`类：

	<ul class="list-group">
	  <li class="list-group-item">First item</li>
	  <li class="list-group-item">Second item</li>
	  <li class="list-group-item">Third item</li>
	</ul>

- `.active`：激活状态列表项
- `.disabled`：禁用列表项
- `.list-group-item-action`：悬停效果，点击背景变为灰色

***

多种颜色列表项：

- `.list-group-item-success`
- `.list-group-item-info`<br>
…………

***

连接列表项：

可以将`<div>`替换`<ul>` ，`<a>`替换`<li>`：（有悬停效果）

	<div class="list-group">
	  <a href="#" class="list-group-item list-group-item-action">First item</a>
	  <a href="#" class="list-group-item list-group-item-success">Second item</a>
	  <a href="#" class="list-group-item list-group-item-info">Third item</a>
	</div>

### 卡片

	<div class="card">
	  <img class="card-img-top" src="img_avatar1.png" alt="Card image">

      <div class="card-header">头部</div>

	  <div class="card-body">
	    <h4 class="card-title">John Doe</h4>
	    <p class="card-text">Some example text.</p>
        <a href="#" class="card-link">Card link</a>
	  </div>

      <div class="card-footer">底部</div>

      <img class="card-img-top" src="img_avatar2.png" alt="Card image">
	</div>

- `.card`
- `.card-header`
- `.card-body`
	- `.card-title`
	- `.card-text`
	- `.card-link`
- `.card-footer`

图片：

- `.card-img-top`：图片在文字上方
- `.card-img-bottom`：图片在文字下方

将图片设为背景：`.card-img-overlay`：

	<div class="card" style="width:500px">
	  <img class="card-img-top" src="img_avatar1.png" alt="Card image">
	  <div class="card-img-overlay">
	    <h4 class="card-title">John Doe</h4>
	    <p class="card-text">Some example text.</p>
	    <a href="#" class="btn btn-primary">See Profile</a>
	  </div>
	</div>

### 下拉菜单：

示例：

	<div class="dropdown">
	  <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
	    Dropdown button
	  </button>
	  <div class="dropdown-menu">
	    <a class="dropdown-item" href="#">Link 1</a>
	    <a class="dropdown-item" href="#">Link 2</a>
	    <a class="dropdown-item" href="#">Link 3</a>
	  </div>
	</div>

- `.dropdown`/`.dropup`：指定一个下拉菜单/或者上拉菜单
- `.dropdown-toggle`、`data-toggle="dropdown"`：在按钮或者链接处添加，用于打开下拉菜单
- `.dropdown-menu`、`.dropdown-item`：设置实际的下拉菜单及其项

在下拉菜单中：

- `.dropdown-divider`：下拉菜单中的分割线<br>
`<div class="dropdown-divider"></div>`
- `.dropdown-header`：下拉菜单中的标题<br>
`<div class="dropdown-header">Dropdown header 1</div>`
- `.dropdown-menu-right`：下拉菜单右对齐
- `.active`/`.disabled`：设置下拉菜单可用项与禁用项

### 折叠

	<button data-toggle="collapse" data-target="#demo">折叠</button>

	<div id="demo" class="collapse">
	Lorem ipsum dolor text....
	</div>

- `data-toggle="collapse"`：指定具有折叠功能的按钮或者链接
- `data-target="#id"`：对应需要折叠的内容
- `.collapse`：指定折叠元素
- `.show`：折叠内容默认隐藏，添加show使其显示

`.data-parent`：

### 导航

	<ul class="nav">
	  <li class="nav-item">
	    <a class="nav-link" href="#">Link</a>
	  </li>
	  <li class="nav-item">
	    <a class="nav-link" href="#">Link</a>
	  </li>
	  <li class="nav-item">
	    <a class="nav-link" href="#">Link</a>
	  </li>
	  <li class="nav-item">
	    <a class="nav-link disabled" href="#">Disabled</a>
	  </li>
	</ul>

- `.nav`
- `.nav-item`
- `.nav-link`

导航对齐方式：默认左对齐

- `.justify-content-center`：导航居中
- `.justify-content-end`：导航右对齐

***

- `.flex-colum`：垂直导航

***

- `class="nav nav-tabs"`：将导航转换为选项卡形式，用`.active`标记

选项卡切换功能：

	<!-- Nav tabs -->
	<ul class="nav nav-tabs">
	  <li class="nav-item">
	    <a class="nav-link active" data-toggle="tab" href="#home">Home</a>
	  </li>
	  <li class="nav-item">
	    <a class="nav-link" data-toggle="tab" href="#menu1">Menu 1</a>
	  </li>
	  <li class="nav-item">
	    <a class="nav-link" data-toggle="tab" href="#menu2">Menu 2</a>
	  </li>
	</ul>

	<!-- Tab panes -->
	<div class="tab-content">
	  <div class="tab-pane active container" id="home">...</div>
	  <div class="tab-pane container" id="menu1">...</div>
	  <div class="tab-pane container" id="menu2">...</div>
	</div>

- `data-toggle="tab"`
- `.tab-content`
- `.tab-pane`

***

- `.nav-pills`：类可以将导航项设置成胶囊形状

***

- `.nav-justified`：可以设置导航项齐行等宽显示

### 导航条

	<nav class="navbar navbar-expand-sm bg-light">

	  <!-- Links -->
	  <ul class="navbar-nav">
	    <li class="nav-item">
	      <a class="nav-link" href="#">Link 1</a>
	    </li>
	    <li class="nav-item">
	      <a class="nav-link" href="#">Link 2</a>
	    </li>
	    <li class="nav-item">
	      <a class="nav-link" href="#">Link 3</a>
	    </li>
	  </ul>

	</nav>

- `.navbar`：定义一个导航栏
- `.navbar-expand-xl|lg|md|sm`：响应式，大屏幕水平铺开，小屏幕垂直堆叠
- `.navbar-nav`、`.nav-item`、`.nav-link`

***

垂直导航条：删除`.navbar-expand-xl|lg|md|sm`

***

- `.navbar-brand`：用于显示品牌logo

***

折叠导航栏：

	<nav class="navbar navbar-expand-md bg-dark navbar-dark">
	  <!-- Brand -->
	  <a class="navbar-brand" href="#">Navbar</a>

	  <!-- Toggler/collapsibe Button -->
	  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
	    <span class="navbar-toggler-icon"></span>
	  </button>

	  <!-- Navbar links -->
	  <div class="collapse navbar-collapse" id="collapsibleNavbar">
	    <ul class="navbar-nav">
	      <li class="nav-item">
	        <a class="nav-link" href="#">Link</a>
	      </li>
	      <li class="nav-item">
	        <a class="nav-link" href="#">Link</a>
	      </li>
	      <li class="nav-item">
	        <a class="nav-link" href="#">Link</a>
	      </li>
	    </ul>
	  </div>
	</nav>

- `.navbar-toggle`、`data-toggle="collapse"`、`data-target="#id"`:设置点击折叠按钮
- `class="collapse navbar-collapse"`：设置需要折叠的导航li

***

- `.form-inline`：导航栏中的表单（内联表单样式）

***

- `.input-group`、`.input-group-addon`

```
    <div class="input-group">
      <span class="input-group-addon">@</span>
      <input type="text" class="form-control" placeholder="Username">
    </div>
```

***

- `.navbar-text`：导航栏上非链接文本

***

- `.navbar-fixed-top`：将导航栏固定在顶部
- `.navbar-fixed-bottom`：将导航栏固定在底部

### 表单

- `.form-inline`：默认堆叠表单，垂直方向；加上此类为内联表单，水平方向。

***

- `<input>`类型：
	- text
	- password
	- datetime
	- datetime-local
	- date
	- month
	- time
	- week
	- number
	- email
	- url
	- search
	- tel
	- color

- `.form-group`
- `.form-control`

```
	<div class="form-group">
	  <label for="usr">用户名:</label>
	  <input type="text" class="form-control" id="usr">
	</div>
```

***

- `<textarea>`：文本域

```
	<div class="form-group">
	  <label for="comment">评论:</label>
	  <textarea class="form-control" rows="5" id="comment"></textarea>
	</div>
```

***

- 复选框（checkbox）
- `.form-check`
- `.form-check-label`
- `.form-check-input`

```
	<div class="form-check">
	  <label class="form-check-label">
	    <input type="checkbox" class="form-check-input" value="">Option 1
	  </label>
	</div>
```

- `.form-check-inline`：让选项显示在同一行上

***

- 单选框：`.redio`
- `.redio-inline`

***

- 下拉菜单（select）

单选下拉菜单：

	<div class="form-group">
	  <label for="sel1">下拉菜单:</label>
	  <select class="form-control" id="sel1">
	    <option>1</option>
	    <option>2</option>
	    <option>3</option>
	    <option>4</option>
	  </select>
	</div>

多选下拉菜单：

	<div class="form-group">
      <label for="sel2">多选下拉菜单(按住 shift 键，可以选取多个选项):</label>
      <select multiple class="form-control" id="sel2">
        <option>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
      </select>
	</div>

### 应用实例：



轮播图：

	<div id="demo" class="carousel slide" data-ride="carousel">

	  <!-- 指示符 -->
	  <ul class="carousel-indicators">
	    <li data-target="#demo" data-slide-to="0" class="active"></li>
	    <li data-target="#demo" data-slide-to="1"></li>
	    <li data-target="#demo" data-slide-to="2"></li>
	  </ul>

	  <!-- 轮播图片 -->
	  <div class="carousel-inner">
	    <div class="carousel-item active">
	      <img src="http://static.runoob.com/images/mix/img_fjords_wide.jpg">
	      <div class="carousel-caption">
	        <h3>第一张图片描述标题</h3>
	        <p>描述文字!</p>
	      </div>
	    </div>
	    <div class="carousel-item">
	      <img src="http://static.runoob.com/images/mix/img_nature_wide.jpg">
	      <div class="carousel-caption">
	        <h3>第二张图片描述标题</h3>
	        <p>描述文字!</p>
	      </div>
	    </div>
	    <div class="carousel-item">
	      <img src="http://static.runoob.com/images/mix/img_mountains_wide.jpg">
	      <div class="carousel-caption">
	        <h3>第三张图片描述标题</h3>
	        <p>描述文字!</p>
	      </div>
	    </div>
	  </div>

	  <!-- 左右切换按钮 -->
	  <a class="carousel-control-prev" href="#demo" data-slide="prev">
	    <span class="carousel-control-prev-icon"></span>
	  </a>
	  <a class="carousel-control-next" href="#demo" data-slide="next">
	    <span class="carousel-control-next-icon"></span>
	  </a>

	</div>

***

模态框：

	<!-- 按钮：用于打开模态框 -->
	<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#myModal">
	  打开模态框
	</button>

	<!-- 模态框 -->
	<div class="modal fade" id="myModal">
	  <div class="modal-dialog modal-sm/-lg">
	    <div class="modal-content">

	      <!-- 模态框头部 -->
	      <div class="modal-header">
	        <h4 class="modal-title">模态框头部</h4>
	        <button type="button" class="close" data-dismiss="modal">&times;</button>
	      </div>

	      <!-- 模态框主体 -->
	      <div class="modal-body">
	        模态框内容..
	      </div>

	      <!-- 模态框底部 -->
	      <div class="modal-footer">
	        <button type="button" class="btn btn-secondary" data-dismiss="modal">关闭</button>
	      </div>

	    </div>
	  </div>
	</div>

***

提示框：

	<a href="#" data-toggle="tooltip" data-placement="top" title="我是提示内容!">鼠标移动到我这</a>
	<a href="#" data-toggle="tooltip" data-placement="bottom" title="我是提示内容!">鼠标移动到我这</a>
	<a href="#" data-toggle="tooltip" data-placement="left" title="我是提示内容!">鼠标移动到我这</a>
	<a href="#" data-toggle="tooltip" data-placement="right" title="我是提示内容!">鼠标移动到我这</a>

	//调用tooltip()方法：
	</script>
	$(document).ready(function(){
	    $('[data-toggle="tooltip"]').tooltip();
	});
	</script>


***

弹出框：

	<div class="container">
	  <h3>弹出框实例</h3>
	  <a href="#" data-toggle="popover" title="弹出框标题" data-content="弹出框内容">多次点我</a>
	</div>

	<script>
	$(document).ready(function(){
	    $('[data-toggle="popover"]').popover();   
	});
	</script>

***

导航栏的滚动监听：`data-spy="scroll" data-target=".navbar"`

垂直滚动监听、水平滚动监听实例。

### 小小工具

- 边框：<br>
边框为蓝色，上边框为0：<br>
`<span class="border border-primary border-top-0"></span>`

***

- 圆角：
```
	<span class="rounded"></span>
	<span class="rounded-top"></span>
	<span class="rounded-right"></span>
	<span class="rounded-bottom"></span>
	<span class="rounded-left"></span>
	<span class="rounded-circle"></span>
	<span class="rounded-0"></span>
```

***

- 浮动：`.clearfix`、`.float-left`、`.float-right`
- 响应式浮动：`.float-sm|md|lg|xl-left|right`

***

- 居中对齐：`.mx-auto`

***

- `w-*`：设置宽度，“ * ”为百分数
- `mw-*`：设置最大宽度
- `h-*`：设置高度
- `mh-*`：最大高度
