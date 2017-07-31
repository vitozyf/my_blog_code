---
title: Ajax
date: 2015-08-01 22:20:35
tags: 
- ajax
categories: 
- js
---

## Ajax过程

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.

(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.

(3)设置响应HTTP请求状态变化的函数.

(4)发送HTTP请求.

(5)获取异步调用返回的数据.

(6)使用JavaScript和DOM实现局部刷新.

## 原生的ajax请求的数据格式

- get: QueryString

- post: 

  - Request Payload 默认

    - Form Data

      通过
      xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
      可以把格式修改为Form Data

## 异步加载和延迟加载

1.异步加载的方案： 动态插入script标签

2.通过ajax去获取js代码，然后通过eval执行

3.script标签上添加defer或者async属性

4.创建并插入iframe，让它异步执行js

5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。

## 请解释一下 JavaScript 的同源策略。

概念:同源策略是客户端脚本（尤其是Javascript）的重要的安全度量标准。它最早出自Netscape Navigator2.0，其目的是防止某个文档或脚本从多个不同源装载。

这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。 指一段脚本只能读取来自同一来源的窗口和文档的属性。

为什么要有同源限制？

我们举例说明：比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。

## GET和POST的区别，何时使用POST？

GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符

POST：一般用于修改服务器上的资源，对所发送的信息没有限制。

GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。

然而，在以下情况中，请使用 POST 请求：
无法使用缓存文件（更新服务器上的文件或数据库）
向服务器发送大量数据（POST 没有数据量限制）
发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

## eval是做什么的？

它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。



## ajax 是什么?ajax 的交互模型?同步和异步的区别?如何解决跨域问题?

1. 通过异步模式，提升了用户体验
2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用
3. Ajax在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载。

## Ajax的最大的特点是什么。

- Ajax可以实现动态不刷新（局部刷新）
- readyState属性 状态 有5个可取值： 0=未初始化 ，1=启动 2=发送，3=接收，4=完成

## ajax的缺点

```
  1、ajax不支持浏览器back按钮。
```

```
  2、安全问题 AJAX暴露了与服务器交互的细节。
```

```
  3、对搜索引擎的支持比较弱。
```

```
  4、破坏了程序的异常机制。
```

```
  5、不容易调试。
```

## AMD和CMD 规范的区别

```
   1、对于依赖的模块，AMD 是提前执行，CMD 是延迟执行
```

```
   2、CMD 推崇依赖就近，AMD 推崇依赖前置
```

## HTTP状态码

```
- 100 ?Continue ?继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
```

```
- 200 ?OK ? 正常返回信息
```

```
- 201 ?Created ?请求成功并且服务器创建了新的资源
```

```
- 202 ?Accepted ?服务器已接受请求，但尚未处理
```

```
- 301 ?Moved Permanently ?请求的网页已永久移动到新位置。
```

```
- 302 Found ?临时性重定向。
```

```
- 303 See Other ?临时性重定向，且总是使用 GET 请求新的 URI。
```

```
- 304 ?Not Modified ?自从上次请求后，请求的网页未修改过。
```

```
- 400 Bad Request ?服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
```

```
- 401 Unauthorized ?请求未授权。
```

```
- 403 Forbidden ?禁止访问。
```

```
- 404 Not Found ?找不到如何与 URI 相匹配的资源。
```

```
- 500 Internal Server Error ?最常见的服务器端错误。
```

```
- 503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
```

## 栈和队列的区别?

```
- 栈的插入和删除操作都是在一端进行的，而队列的操作却是在两端进行的。队列先进先出，栈先进后出。
```

```
- 栈只允许在表尾一端进行插入和删除，而队列只允许在表尾一端进行插入，在表头一端进行删除 
```

```
- 栈和堆的区别？
```

```
- 栈区（stack）—   由编译器自动分配释放   ，存放函数的参数值，局部变量的值等。
- 堆区（heap）   —   一般由程序员分配释放，   若程序员不释放，程序结束时可能由OS回收。

- 堆（数据结构）：堆可以被看成是一棵树，如：堆排序；

- 栈（数据结构）：一种先进后出的数据结构。 
```

## XML和JSON的区别？

```
- (1).数据体积方面。
	JSON相对于XML来讲，数据的体积小，传递的速度更快些。
- (2).数据交互方面。
	JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互。
- (3).数据描述方面。
	JSON对数据的描述性比XML较差。
- (4).传输速度方面。
	JSON的速度要远远快于XML。
```

## 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？

```
分为4个步骤：
```

```
（1），当发送一个URL请求时，不管这个URL是Web页面的URL还是Web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址。
```

```
（2）， 浏览器与远程Web服务器通过TCP三次握手协商来建立一个TCP/IP连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
```

```
（3），一旦TCP/IP连接建立，浏览器会通过该连接向远程服务器发送HTTP的GET请求。远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。
```

```
（4），此时，Web服务器提供资源服务，客户端开始下载资源。
请求返回后，便进入了我们关注的前端模块
简单来说，浏览器会解析HTML生成DOM Tree，其次会根据CSS生成CSS Rule Tree，而javascript又可以根据DOM API操作DOM
```

## ajax加载的页面，跳转到另外一个页面再跳转回来，内容相同，如何节约读取请求?

```
答：后台做缓存，读取缓存里面的数据。CDN
```

## 跨域访问

1. 跨域访问.
   ​      
   以ajax发起跨域请求,浏览器是不允许的. ajax只能向同源资源发起请求.

2. 如何实现跨域请求.

   ```
    - ajax无论如何是不行的.
   ```

   ```
    - script标签.
   ```

   ```
          CDN. 内容分发网络.
          网站引入的js文件是很多的.
          大多数都是一些第三方库.
          jq
          bots
          ang
          如果把这些文件都放在自己的服务器上 无疑会增大服务器的压力.

          怎么办？
          有一些好心的机构。
          他们自己搭建搭建了一些服务器. 在他们的服务器上放了一些常用的库.
          CDN.
   ```

   - script的src属性是天然支持跨域的.

------

### 实现

1. script标签将src指向的js文件请求过来以后 他会将其执行一次.
2. src属性可以请求任意格式的文件.
   无论是什么文件 请求过来的数据 都会当做js代码执行一次.
3. 利用script的src属性来实现跨域请求 - jsonp
   - 3.1 准备1个函数 这个函数至少带1个参数.
   - 3.2 创建1个script标签.
     利用src属性发起跨域请求.将函数名称发给服务器.
   - 3.3 服务器:
     处理数据.
     去除浏览器发给我的函数的名称.
     返回: 函数名称(真正的数据)
   - 3.4 浏览器拿到返回的数据 就当做js代码执行.
     我们事先准备的函数就被执行了.
     函数的参数就是服务器真正给我的数据.

------

```
	  //封装jsonP
    function jsonP(opts) {
        opts.url += "?";
        for (var key in opts.data) {
            opts.url += key + "=" + opts.data[key] + "&";
        };
        var callbackName = "jsonP" + Math.random().toString().slice(2);
        window[callbackName] = opts.success;
        opts.url += "callback=" + callbackName;
        var script = document.createElement('script');
        script.src = opts.url;
        document.body.appendChild(script);
    }
		//使用
	  window.onload = function() {
        jsonP({
            url: "http://api.map.baidu.com/telematics/v3/weather",
            data: {
                ak: "0A5bc3c4fb543c8f9bc54b77bc155724",
                location: "深圳",
                output: "json"
            },
            success: function(res) {
                console.log(res);
            }
        })
    }
```