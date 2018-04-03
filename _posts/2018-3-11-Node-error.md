---
layout: post
title: "Node.js遇到的错误"
date: 2018-03-11
description: "node开发，打包js文件，执行npm run build命令时，遇到的错误及解决方法"
tag: node
---  
## npm run build（打包报错）

	F:\GitHub\test\simple-app-demo>npm run build

	> simple-app-demo@1.0.0 build F:\GitHub\test\simple-app-demo
	> webpack app.js bundle.js

	F:\GitHub\test\simple-app-demo\node_modules\webpack\bin\webpack.js:3
	let webpackCliInstalled = false;
	^^^

	SyntaxError: Block-scoped declarations (let, const, function, class) not yet supported outside strict mode
	    at exports.runInThisContext (vm.js:53:16)
	    at Module._compile (module.js:373:25)
	    at Object.Module._extensions..js (module.js:416:10)
	    at Module.load (module.js:343:32)
	    at Function.Module._load (module.js:300:12)
	    at Function.Module.runMain (module.js:441:10)
	    at startup (node.js:139:18)
	    at node.js:968:3

	npm ERR! Windows_NT 10.0.10240
	npm ERR! argv "F:\\nodejs\\node.exe" "F:\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "run" "build"
	npm ERR! node v4.4.3
	npm ERR! npm  v2.15.1
	npm ERR! code ELIFECYCLE
	npm ERR! simple-app-demo@1.0.0 build: `webpack app.js bundle.js`
	npm ERR! Exit status 1
	npm ERR!
	npm ERR! Failed at the simple-app-demo@1.0.0 build script 'webpack app.js bundle.js'.
	npm ERR! This is most likely a problem with the simple-app-demo package,
	npm ERR! not with npm itself.
	npm ERR! Tell the author that this fails on your system:
	npm ERR!     webpack app.js bundle.js
	npm ERR! You can get information on how to open an issue for this project with:
	npm ERR!     npm bugs simple-app-demo
	npm ERR! Or if that isn't available, you can get their info via:
	npm ERR!
	npm ERR!     npm owner ls simple-app-demo
	npm ERR! There is likely additional logging output above.

	npm ERR! Please include the following file with any support request:
	npm ERR!     F:\GitHub\test\simple-app-demo\npm-debug.log



### 错误1：SyntaxError: Block-scoped declarations (let, const, function, class) not yet supported outside strict mode
- 原因：node版本太低，不支持ES6写法
- 解决方法：更新node至最新版本<br>
在官网上下载node最新版本的msi，点击安装，安装路径为原来路径，将原来node版本覆盖

### 错误2：npm ERR! Windows_NT 10.0.10240

- 原因：由于Node的官方模块仓库网速太慢，模块仓库切换到了阿里的源
- 使用了淘宝的cnpm：这样的话不要输入npm用cnpm来代替

### 错误3：The CLI moved into a separate package: webpack-cli.
解决错误1、2后：

	F:\GitHub\test\simple-app-demo>cnpm run build

	> simple-app-demo@1.0.0 build F:\GitHub\test\simple-app-demo
	> webpack app.js bundle.js

	The CLI moved into a separate package: webpack-cli.
	Please install 'webpack-cli' in addition to webpack itself to use the CLI.
	-> When using npm: npm install webpack-cli -D
	-> When using yarn: yarn add webpack-cli -D
	npm ERR! code ELIFECYCLE
	npm ERR! errno 1
	npm ERR! simple-app-demo@1.0.0 build: `webpack app.js bundle.js`
	npm ERR! Exit status 1
	npm ERR!
	npm ERR! Failed at the simple-app-demo@1.0.0 build script.
	npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

	npm ERR! A complete log of this run can be found in:
	npm ERR!     C:\Users\胡煦\AppData\Roaming\npm-cache\_logs\2018-03-29T09_23_44_212Z-debug.log

- 解决方法：命令行输入-->`npm install webpack-cli -D`，安装`webpack-cli`

### 错误4：
接着又出现了新的错误：

	ERROR in multi ./app.js bundle.js
	Module not found: Error: Can't resolve 'bundle.js' in 'F:\GitHub\test\simple-app-demo'
	 @ multi ./app.js bundle.js
	npm ERR! code ELIFECYCLE
	npm ERR! errno 2
	npm ERR! simple-app-demo@1.0.0 build: `webpack app.js bundle.js`
	npm ERR! Exit status 2
	npm ERR!
	npm ERR! Failed at the simple-app-demo@1.0.0 build script.
	npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

	npm ERR! A complete log of this run can be found in:
	npm ERR!     C:\Users\胡煦\AppData\Roaming\npm-cache\_logs\2018-03-29T13_09_52_031Z-debug.log

- 原因：webpack 4 之后这个命令已经不行，需要命令行指明output-filename 和 output-path
- 解决方法：`package.json`中<br>将`"build": "webpack app.js bundle.js`改成`"build": "webpack app.js --output-filename bundle.js  --output-path . --mode development"`

**终于打包成功！！！**
