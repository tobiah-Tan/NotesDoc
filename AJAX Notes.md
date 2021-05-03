# AJAX Notes

## 一、原生Ajax

### 1.1 Ajax简介

- Ajax 全称为 Asynchronous JavaScript and XML，就是异步的JS和XML
- 通过Ajax可以在浏览器中向服务器发送异步请求，最大的优势：**无刷新获取数据**
- Ajax不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式

### 1.2 XML简介

- XML可扩展标记语言

- XML被设计用来传输和存储数据

- XML和HTML类似，不用的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据

  ```xml
  <student>
      <name>孙悟空</name>
      <age>18</age>
  </student>
  ```

  现在已经被json取代了

### 1.3 Ajax-HTTP协议请求报文与响应文本结构

- HTTP

  HTTP(hypertext transport protocol) 协议[超文本传输协议]，协议详细规定了浏览器和万维网服务器之间互相通信的规则。约定，规则

  - 请求报文

    （重点是格式与参数）

    - 行			POST(GET)	/s?ie=utf-8		HTTP/1.1

    - 头            HOST: atguigu.com

      ​				Cookie: name=guigu

      ​				Content-type: application/x-www-form-urlencoded

      ​				User-Agent: chrome 83

    - 空行        

    - 体            username=admin&password=admin

  - 响应报文

    - 行			HTTP/1.1	200	OK

    - 头            Content-Type:text/html;charset=utf-8

      ​				Content-length:2048

      ​				Content-encoding:gzip

    - 空行         

    - 体            <html>

      ​						<head>

      ​						</head>

      ​						<body>

      ​								<h1>Ajax笔记</h1>

      ​						</body>

      ​				</html>

## 二、跨域

### 2.1 jsonp

- JSONP是什么？

  - JSONP(JSON with Pading)，是一个非官方的跨域解决方案，只支持 get 请求。

- JSONP 怎么工作的？

  - 在网页有一些标签天生具有跨域能力，比如：img link iframe script
  - JSONP 就是利用 script 标签的跨域能力来发送请求的。

- JSONP 的使用

  - 动态的创建一个 script 标签

    ```js
    var scipt = document.creatElemnt("script");
    ```

  - 设置 script 的 src，设置回调函数

    ```js
    script.src = "htp:/localhost:30/tesAJX?calback=abc";
    function abc(dat) {
    	alert(dat.name);
    };
    ```

  - 将 script 添加到 body 中

    ```js
    document.body.apendChild(script);
    ```

  - 服务器中路由的处理

    ```js
    router.get("/tesAJX" , function (req , res) {
    	console.og("收到请求"); 
    	var calback = req.uery.calback; 
    	var obj={
    		name:"孙悟空", age:18
    	}
    	res.end(calback+"(+JSON.stringfy(obj)+");
    });
    
    ```

    