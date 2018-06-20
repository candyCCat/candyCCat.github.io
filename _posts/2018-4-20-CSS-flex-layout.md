---
layout: post
title: "Flex弹性布局"
date: 2018-04-20
description: ""
tag: CSS
---  

&emsp;&emsp;传统的前端页面布局：基于`盒模型`，依赖于`display`、`float`、`position`属性，对于那些特殊的布局很不方便。现在有了`flex`，让布局变得更简单。目前，它得到所有浏览器的支持，使开发更简便！

### 基本概念

- `Flexible Box`：弹性布局，为盒模型提供灵活布局；
- `flex容器`中有几概念：
	- `flex项目`：flex容器包裹flex项目
	- `主轴`：默认水平方向，从左到右
	- `侧轴`：默认垂直方向，从上到下
- 指定一个弹性布局盒子：

```
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
```

*注意：设为`Flex`布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。*

### flex container容器属性

- `flex-direction`：设置主轴方向，即项目的排列方向；<br>
例：`flex-direction: row | row-reverse | column | column-reverse;`
	- `row`（默认）：主轴为水平方向，从左向右；
	- `row-reverse`：水平方向，从右向左；
	- `column`：垂直方向，从上到下；
	- `column-reverse`：垂直方向，从下到上。

***

- `flex-wrap`：设置项目的换行方式；<br>
例：`flex-wrap: nowrap | wrap | wrap-reverse;`
	- `nowrap`（默认）：如果项目一行排不下，不换行；
	- `wrap`：换行，第二行在下方；
	- `wrap-reverse`：换行，第二行在上方。

***

- `flex-flow`：`flex-direction`+`flex-wrap`的简写；<br>
默认：`flex-flow: row nowrap;`

***

- `justify-content`：定义项目在主轴上的对齐方式<br>
例：`justify-content: flex-start | flex-end | center | space-between | space-around;`<br>
假设主轴`row`，水平从左到右：
	- `flex-start`（默认）：左对齐；
	- `flex-end`：右对齐；
	- `center`：居中；
	- `space-between`：两端对齐，项目之间间隔相等；
	- `space-around`：每个项目两侧都有间隔且相等。


***

- `align-items`：项目在侧轴上的对齐方式；<br>
例：`align-items: flex-start | flex-end | center | baseline | stretch;`
	- `flex-start`：侧轴起点对齐；
	- `flex-end`：侧轴终点对齐；
	- `center`：居中；
	- `baseline`：项目第一行文字的`基线`对齐；
	- `stretch`：如果项目高度为`auto`，将其拉伸占满容器高度。

***

- `align-content`：项目有多根轴线（多行）的对齐方式；<br>
例：`align-content: flex-start | flex-end | center | space-between | space-around | stretch;`

### flex item项目属性

- order：默认0，设置item的排列顺序，数值越小越靠前；
- flex-grow：默认0，设置item的放大比例；0：不伸缩，其他数字按比例伸缩；
- flex-shrink：默认1，设置item缩小比例；0：不伸缩；
- flex-basis：为项目设置宽度用到；
- flex：`flex-grow`+`flex-shrink`+`flex-basis`的简写，默认：`0 1 auto`；
- align-self：设置单个item与其他item不一样的侧轴对齐方式；<br>
`align-self: auto | flex-start | flex-end | center | baseline | stretch;`
