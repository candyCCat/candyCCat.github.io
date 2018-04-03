---
layout: post
title: "GitHub Pages和Jekyll博客搭建"
date: 2018-03-27
description: "windows环境下基于GitHub Pages和Jekyll的个人博客搭建"
tag: 工具
---   


参考：[https://segmentfault.com/a/1190000012468796](https://segmentfault.com/a/1190000012468796)<br>
&emsp;&emsp;&emsp;[https://blog.csdn.net/rainloving/article/details/45745491](https://blog.csdn.net/rainloving/article/details/45745491)

## 一、建立github站点
&emsp;&emsp;参考：[https://pages.github.com/](https://pages.github.com/)<br>
&emsp;&emsp;步骤相对简单，就是按照规定的命名格式新建一个github`repository`，便能使github page运行起来。
## 二、在windows上安装Jekyll
&emsp;&emsp;`Jekyll`是一个简单的免费的Blog生成工具，类似`WordPress`。但是和`WordPress`又有很大的不同，`jekyll`只是一个生成静态网页的工具，不需要数据库支持。最关键的是jekyll可以免费部署在`Github`上，并且绑定自己的域名。
### 1.安装Ruby
#### 首先需要知道为什么安装Ruby？
- `ruby`是一种脚本语言；
- `rubygems`是`ruby`的一个包管理器，简称`gem`<br>*(ruby 1.9.2及其以上就已经默认安装了ruby gem的，所以无需再次手动安装)*
- `ruby bundler`(rails框架中用来管理多版本的gem的，叫bundle)，在windows中搭建jekyll，需要安装完ruby后用gem安装下bundler
- `jekyll`是基于`ruby`的，所以搭建`jekyll`之前必须确保`ruby`正常安装<br>***注意**：ruby大于2.0.0*

#### Ruby的安装

1. 前往：[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)下载相应版本；我选择的是`Ruby 2.3.3-2(x64)`.<br>
2. 最好保持默认路径`C:\Ruby24-x64`;<br>选择`Add Ruby executables to your PATH`添加环境变量<br>![](/images/posts/180327/Ruby1.png)
3. Ruby安装完成之后，打开cmd，输入`ruby -v`，查看ruby版本，如果显示ruby版本号，说明安装成功。<br>![](/images/posts/180327/Ruby2.png)


### 2.安装DevKit
&emsp;&emsp;`DevKit`是一个在Windows上帮助简化安装及使用`Ruby C/C++`扩展如：`RDiscount`和`RedCloth`的工具箱。

1. 再次前往：[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)下载系统及Ruby适应版本的DevKit安装包；我选择`DevKit-mingw64-64-4.7.2-20130224-1432-sfx`;
2. 点击安装，并解压至文件夹`C:\DevKit`<br>![](/images/posts/180327/Ruby3.png)
3. 安装完成后，通过初始化来创建`config.yml`文件；<br>在cmd中输入命令行：<br>`cd C:\DevKit`进入文件夹；<br>`ruby dk.rb init`运行完毕自动生成`config.yml`文件；<br>![](/images/posts/180327/Ruby4.png)
4. 接下来编辑这个文件，在文件的末尾添加一行`- c:\Ruby23-x64`，这里`- c:\Ruby23-x64`是实际ruby安装的文件名及路径。
5. 修改完成后，键入命令行`ruby dk.rb install`即可。<br>![](/images/posts/180327/Ruby5.png)
6. 一切顺利后，Development Kit已经正确安装并配置。

### 3.安装Jekyll
1. 键入命令行：<br>`gem -v`：gem正确安装输出版本号；<br>`gem install bundler`：前面已经解释到bundler；<br>`gem install jekyll`：安装Jekyll。<br>![](/images/posts/180327/Ruby6.png)
2. **修改默认source源**：<br>官方源无法访问，所以我们得更换为可以使用的源，这里推荐使用[ruby china](http://gems.ruby-china.org)
	- 键入命令`gem sources -l`(*注意这里是l，而不是1*)：查看当前已经添加的源；
	- `gem sources -r https://rubygems.org/`：移除官方源；<br>*注：这里移除上一步查询到的源，以实际为准*
	- `gem sources -a http://gems.ruby-china.org`：添加[ruby china](http://gems.ruby-china.org)源；
	- 修改后，通过`gem sources -l`查看修改是否正确。
3. 出现如下错误，在命令行中键入`bundle install`<br>![](/images/posts/180327/Ruby7.png)

### 4.Jekyll博客搭建
1. 搭建jekyll环境，其实是提供了一个本地服务器，有可预览博客网页效果的作用。<br>[Jekyll中文官网](https://www.jekyll.com.cn/)<br>[Jekyll主题模板](http://jekyllthemes.org/)
2. 使用模板：<br>&emsp;&emsp;如果你是前端开发人员，想自己写博客主题页面，可以在`github pages repository`里从零开始写代码；但如果你只是想专注博客内容，完全可以找到一个自己喜欢的Jekyll模板，将其fork改造，作为自己的博客模板。
3. jekyll博客预览：
	- 打开cmd，进入本地博客仓库文件夹；<br>**注意**：文件夹路径不能带有中文字符，否则会出现编码错误，如下：<br>![](/images/posts/180327/Ruby8.png)
	- 在确保安装好`jekyll`和`bundler`后（"`gem install jekyll bundler`"），键入`jekyll serve`<br>![](/images/posts/180327/Ruby9.png)
	- 运行成功！在浏览器中输入`http://localhost:4000`可预览博客效果。
