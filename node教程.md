# node教程

## 创建第一个应用

- 在使用node.js时，我们不仅仅在实现一个应用，同时还在实现整个http服务器。我们的Web应用以及对应的web服务器基本上是一样的

- Node.js由三部分组成

  - 引入required模块
  - 创建服务器
  - 接收请求和响应请求

- 创建node.js应用

  - 1.引入required模块

    ```JavaScript
    var http = require("http")；// 使用require指令来载入http模块
    ```

  - 2.创建服务器

    ```javascript
    var http = require("http");
    
    http.creatServer(function(request,response)
    {
    	// 发送 http 头部
    	// HTTP状态码
    	// 内容类型：text/plain
    	response.witheHead(200,{'content - type':'text/plain'}); // 状态码和内容
    	response.end("hello world\n");
    }).listen(8888);
    
    consol.log("servering!!!")
    ```

    

## npm使用介绍

- npm是和node.js一起安装的包管理工具

  - 允许用户从npm服务器下载别人编写的第三方包到本地使用
  - 允许用户从npm服务器下载并安装别人编写的命令行程序到本地使用
  - 允许用户将自己编写的包或行程序上传到npm服务器上

- 使用npm命令安装模块

  - ```shell
    npm install <module Name>
    ```

- 使用JavaScript使用该模块

  - ```javascript
    var express = require("express");
    ```

- 全局安装和本地安装

  - ```shell
    npm install express #本地安装
    npm install express -g #全局安装
    ```

  - 本地安装

    - 会将安装包放在./node_modules 下
    - 可以通过require()来引入本地安装包

  - 全局安装

    - 将安装包放在/usr/local下或者node的安装目录中
    - 可以直接在命令行中使用

  - 如果你希望具备两种功能，这需要在两个地方安装他或者使用npm link

## REPL（交互解释器）

- 表示一个环境，类似终端

- REPL可以执行以下任务

  - 读取
  - 执行
  - 打印
  - 循环

- 输入node启动

  - 简单的表达式运算
  - 使用变量
  - 多行表达式
  - 下划线变量，可以使用下划线来获取上一个表达式的运算结果

- REOPL命令

  ![image-20210128152245599](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210128152245599.png)

  

## node.js回调函数

- node.js异步编程的直接体现就是回调

- 异步编程依托回调来实现，但是不能所使用了回调后程序就异步化了

- 回调函数在完成任务后就会被调用，Node使用了大量的回调函数，node的所有api都支持回调函数

- 我们一边读取文件，一边执行其他命令，文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件i/o操作。这大大提高了node.js的性能，可以处理大量的并发请求

- 回调函数一般作为函数的最后一个函数出现

  ```javascript
  function fool(name,age,callback){}
  function foo2(value,callback,callback2){};
  
  // 其中callback()和callback2()都是作为回调函数出现
  ```

- 阻塞代码示例

  - 1.创建一个文件

  - 2.js代码

    ```javascript
    var fs = require('fs'); // 获取相应模块
    var data = fs.readFileSync('input.txt'); // 读取文件
    
    console.log(data.toString());
    console.log("程序结束")；
    ```

- 非阻塞代码示例

  - 1.创建文件

  - 2.js代码

    ​	

    ```JavaScript
    var fs = require("fs");
    
    fs.readFile("input.txt",function(err,data){
    if(err)return consol.error(err); // 这里出现错误就结束该程序
    consol.log(data.toString());
    })
    consol.log("程序执行结束")；
    ```

- 阻塞代码是按顺序执行的，而非阻塞表示按顺序执行的

- 数据的处理在回调函数内

## node.js 事件循环

- Node.js是单进程但线程应用程序，但是以为v8引擎提供的异步执行的回调接口，通过这些接口可以处理大量的并发，所有性能非常的高

- Node.js几乎每一个API都是支持回调函数的

- Node.js基本上的所有的事件机制都是用设计模式中的观察模式

- Node.js单线程类似进入一个while(true)的时间循环，直到没有事件观察者退出，每一个异步事件都会生成一个事件观察者。如果有事件发生就调用该回调函数

- 事件循环程序

  - Node.js使用事件驱动模型，当web server接收到请求，就把它关闭然后进行处理，然后去服务下一个web请求

  - 当完成这个请求，它会被放回处理队列，当到达队列开头，这个结果就返回用户

  - 这个模型非常高效可扩展性非常高，因为webserver一直接收请求而不等待任何读写操作。（这被称为非阻塞io或者事件驱动io）

  - 在事件驱动模型中，会生成一个主循环来监听事件，当检测到事件时就会触发回调函数

    ![image-20210128155348573](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210128155348573.png)

  - node.js有多个内置的事件，我们可以通过引入events模块，并通过实例化EventEmitter类来绑定和监听事件，如下例：

    ```javascript
    var events = require('event'); // 引入events模块
    var eventEmitter = new events.EventEmitter(); // 创建eventEmitter对象
    
    eventEmitter.on("eventName",eventHandler); // 绑定事件处理程序
    eventEmitter.emit('eventName'); // 绑定事件
    ```

  - 实例

    ```javascript
    var events = require('events');
    
    var eventEmitter = new events.EventEmitter();
    
    var connectHandler = function connected(){
    	console.log("连接成功");
    	
    	// 触发data_received 事件
    	eventEmitter.emit('data_received');
    }
    
    eventEmitter.on('connection',connectHandle);
    
    eventEmitter.emit('connection'); // 触发事件
    
    console.log("程序执行完毕")；
    ```

- node应用程序是如何工作的？？

  - 在node应用程序中，执行异步操作的函数将回调函数作为最后一个参数，回调函数接收错误对象作为第一个参数

  - 实例

    ```javascript
    var fs = require('fs');
    fs.readFile('input.txt',function(err,data){
    	if(err){
    		console.log(err.stack);
    		return;
    	}
    	console.log(data.toString());
    });
    	consol.log("程序执行完毕");
    ```

## EventEmitter

- node.js所有的异步i/o操作在完成时都会发送一个事件到事件队列
- node.js里面的许多对象都会分发事件：一个net.Server对象会在每次有新连接时触发一个新事件，一个fs.readStream对象会在文件被打开的时候触发一个事件。所有的这些事件的对象都是events.EventEmitter的实例。
- EventEmitter类
  - event模块只提供了一个对象：events.EventEmitter。EventEmitter的核心就是事件触发和事件监听器功能的封装                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

