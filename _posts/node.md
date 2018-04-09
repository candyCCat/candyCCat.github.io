

## 零碎点

### 定义全局变量
`global.dbHelper = require( './common/dbHelper' )`：这样dbHelper就可以在任何模块内调用。

`global.db = mongoose.connect("mongodb://127.0.0.1:27017/test")`：数据库的连接也需要定义全局变量

### node.js文件中：console.log中文乱码问题

问题：node的`.js`文件中，当`console.log("中文")`时，控制台输出会出现乱码现象。

原因：`.js`文件是以GBK的编码格式保存，？？至于为什么暂时没理清内因，待续…………

解决方法：确保`.js`文件是tuf-8编码格式

