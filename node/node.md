## （一）node基础

### 一、什么是Node.js

​	Node.js是一个基于 Chrome V8 引擎的 JavaScript 运行环境

### 二、Node.js 可以做什么

1. 基于Express 框架（http://www.expressjs.com.cn/），可以快速构建web应用
2. 基于Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用
3. 基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目
4. 读写和操作数据库，创建实用的命令行工具辅助前端开发。。。

### 三、什么是 fs 文件系统模块

​	**fs 模块** 是 用来操作文件的模块

+ js.readFile() 方法，用来读取指定文件中的内容
+ js.writeFile() 方法，用来向指定的文件中写入内容

#### 执行代码

```
// 导入 fs 文件模块
const fs = require('fs')

// 读取指定文件中的内容
fs.readFile(path[,options],callback)

// 向指定文件中写入内容
fs.writeFile(file,data[,options],callback)
```

​		path：表示文件路径

​		data：表示要写入的内容

​		options：表示以什么编码格式来读取文件（utf8）

​		callback：通过回调函数拿到读取的结果

#### 路径动态拼接

__dirname 表示当前文件所处的目录

### 四、什么是 path 路径模块

​	path 模块 是用来 处理路径 的模块

+ path.join() ，用来将多个路径片段拼接成一个完整的路径字符串
+ path.basename()，用来从路径字符串中，将文件解析出来

#### 执行代码

```
// 导入 path 模块
const path = require('path')
```

#### path.join() 获取路径

![1657516210853](E:\笔记\node\assets\1657516210853.png)

#### path.basename() 获取文件名

![1657516886298](E:\笔记\node\assets\1657516886298.png)

#### path.extname() 获取文件扩展名

![1657517197435](E:\笔记\node\assets\1657517197435.png)

### 五、什么是 http 模块

​	http模块 是用来创建 web 服务器的 模块

```
// 1.导入 http 模块
const http = require('http')

// 2.创建 web 服务器实例
const server = http.createServer()

// 3.为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
    console.log('Some visit our web server');
})


// 4.启动服务器
server.listen(80, function () {
    console.log('server running at http://127.0.0.1');
})
```

#### 	req 请求对象

​		只要服务器收到了客户端你的请求，就会调用通过 **sever.on()**  为服务器绑定的 request事件处理函数

#### 	res响应对象

​	访问与服务器相关的数据或属性，

​	向客户端发送指定的内容，并结束请求的处理过程

#### 	解决中文乱码的问题

```
// 为了防止中文显示乱码的问题，需要设置响应头
    res.setHeader('Content-Type','text/html; charset=utf-8')
```

### 六、根据不同的 url 响应不同的 html 内容

#### 	1.核心步骤

![1657525642152](E:\笔记\node\assets\1657525642152.png)

## （二）Node.js中的模块化

### 	一、分类

+ 内置模块（由node.js官方提供的，如：fs、path、http等）
+ 自定义模块（用户创建的每一个.js文件，都是自定义模块）
+ 第三方模块（由第三方开发出来的模块）

### 	二、加载模块

​	require()

![1657530916332](E:\笔记\node\assets\1657530916332.png)

### 	三、模块作用域

​	只能在当前模块内被访问

### 	四、向外共享模块作用域中的成员

#### 	module对象

​		存储了和当前模块有关的信息

#### 	module.exports对象 

​		将模块内的成员共享出去

#### 	exports对象

​		作用同上

## （三）包（第三方模块）

​	[https://www.npmjs.com/](https://www.npmjs.com/)

### 	一、格式化时间

​		格式化时间的包 **moment**

![1657542849167](E:\笔记\node\assets\1657542849167.png)

### 	二、在项目中安装包的命令

![1657542917730](E:\笔记\node\assets\1657542917730.png)

### 	三、初次装包后的文件

​	**node_modules** 文件夹用来存放所有安装到项目的包

​	**package-lock.json** 配置文件 用来记录node_modules 目录下的每一个包的下载信息

### 	四、安装指定版本的包

![1657543498592](E:\笔记\node\assets\1657543498592.png)

### 	五、包管理配置文件

​	package.json 包管理配置文件，用来记录与项目有关的一些配置信息

##### 		1.快速创建 package.json

![1657543705532](E:\笔记\node\assets\1657543705532.png)

​		**注意：**不能有中文和空格

##### 		2.dependencies节点

​		记录在安装了哪些包

### 	六、一次性安装所有的包

```
npm install
npm i
```

### 	七、卸载包

```
npm uninstall
```

![1657544254280](E:\笔记\node\assets\1657544254280.png)

### 	八、devDependencies 节点（核心依赖包）

![1657544337949](E:\笔记\node\assets\1657544337949.png)

### 	九、淘宝 NPM 镜像服务器

#### 		1.切换 npm 的下包镜像源

```
//查看当前的下包镜像源
npm config get registry
//将下包的镜像源切换为淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
//检查镜像源是否下载成功
npm config get registry
```

#### 		2.nrm

```
//通过 npm 包管理器，将nrm 安装为全局可用的工具
npm i nrm -g
//查看所有可用的镜像源
nrm ls
//将下包的镜像源切换为 taobao 镜像
nrm use taobao
```

## （三）包的分类

#### 	1、项目包

+ **开发依赖包**：devDependencies ，开发期间可用
+ **核心依赖包**：dependencies，开发和项目上线都可用

#### 	2、全局包

​	在执行npm install 命令时，如果提供了 **-g** 参数，则会把包安装为全局包

```
安装位置：
C:\Users\PLA\AppData\Roaming\npm\node_modules
```

![1657545586470](E:\笔记\node\assets\1657545586470.png)

#### 	3、i5ting_toc

​	可以把 md 文档转为 html 页面的工具

![1657545682782](E:\笔记\node\assets\1657545682782.png)

