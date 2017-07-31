---
title: HTML5
date: 2015-08-19 22:33:25
tags: 
- h5
categories: 
- html
---

# ＨTML５

## Ｈ５新元素

- HTML5定义了一系列新元素，如新语义标签、智能表单、多媒体标签等，可以帮助开发者创建富互联网应用，还提供了一些Javascript API，如地理定位、重力感应、硬件访问等，可以在浏览器内实现类原生应用，甚至结合Canvas我们可开发网页版游戏。

- 广义概念：HTML5代表浏览器端技术的一个发展阶段。在这个阶段，浏览器呈现技术得到了一个飞跃发展和广泛支持，它包括：HTML5，CSS3，Javascript，API在内的一套技术组合 。

- 优点：[http://www.intertid.com/school/2014/595568.shtml](http://www.intertid.com/school/2014/595568.shtml)

  ### 语法规则

- 去除了许多冗余的内容，书写规则更加简洁、清晰。

### 语义标签

- HTML5增加了大量更有意义的语义标签，更有利于搜索引擎或辅助设备理解HTML页面内容。
  - 统的做法我们或许通过增加类名如class="header"、class="footer"，使HTML页面具有语义性，但是**不具有通用性**。
  - HTML5则是通过新增语义标签的形式来解决这个问题，例如`<header></header>、<footer></footer>`等，这样就可以使其**具有通用性**。

### 新增只能表单元素

伴随着互联网富应用以及移动开发的兴起，传统的Web表单已经越来越不能满足开发的需求，所以HTML5在Web表单方向也做了很大的改进，如拾色器、日期/时间组件等，使表单处理更加高效。

- email url search(搜索框，更具语义化) range（自由拖动滑块） date（日期）
- 表单属性
  - placeholder 占位符
  - autofocus 自动获得焦点
  - required 必须填入内容
  - pattern 自定义验证
- **部分类型是针对移动设备生效的，且具有一定的兼容性，在实际应用当中应选择性的使用**

### 多媒体

- HTML5通过`<audio>`标签来解决音频播放的问题。

  - autoplay 自动播放
  - controls 是否显不默认播放控件
  - loop 循环播放
  - preload 预加载 同时设置autoplay时此属性失效

- 多浏览器支持的方案：通过soutce标签指定多格式音频文件

  <audio controls>

  ```
  	<source src="see.mp3">
  	<source src="see.wav">
  	<source src="see.ogg">
  	您的浏览器不支持HTML音频播放功能
  </audio>
  ```

- HTML5通过`<video>`标签来解决音频播放的问题。

  - autoplay 自动播放
  - controls 是否显示默认播放控件
  - loop 循环播放
  - preload 预加载，同时设置了    
  - autoplay，此属性将失效
  - width 设置播放窗口宽度
  - height 设置播放窗口的高度

- 多浏览器支持的方案：通过soutce标签指定多格式音频文件

  <video controls>

  ```
  	<source src="see.ogg">
  	<source src="see.mp4">
  	您的浏览器不支持HTML视频播放功能
  </video>
  ```

### dom扩展

- 获取元素
  - document.querySelector('div')
  - document.querySelectorAll('selector')
- 类名操作
  - 1、Node.classList.add('class') 添加class
  - 2、Node.classList.remove('class') 移除class
  - 3、Node.classList.toggle('class') 切换class，有则移除，无则添加
  - 4、Node.classList.contains('class') 检测是否存在class
  - Node指一个有效的DOM节点，是一个统称。
- 自定义属性
  - 在HTML5中我们可以自定义属性，其格式如下data-*=""，例如
    data-info="我是自定义属性"，通过Node.dataset['info'] 我们便可以获取到自定义的属性值。
  - Node.dataset是以类对象形式存在的

### 网络状态

- 网络状态：navigator.online;返回一个boolean类型

  - 用来检测用户是否联网，不仅仅指的是链接外网，连接了局域网也算，甚至本机和虚拟机的网卡链接起来，也算是一个网络连接状态
  - 注意：返回true不一定就是说一定能访问互联网，因为有可能连接的是局域网。但是返回false则表示一定连不上网。

- 监听网络状态

  - 为了更好的确定网络是否连接，HTML5还定义了两个事件，用于监听网络状态的变化。

    //网络连接时会被调用

    ```
     window.addEventListener("online", function () { 
    alert("online"); 
    }); 
    //网络断开时会被调用
    window.addEventListener("offline", function () {
     alert("offline");
     });
    ```

### 地理位置

- 在HTML规范中，增加了获取用户地理信息的API，这样使得我们可以基于用户位置开发互联网应用，即基于位置服务LBS(Location Base Service)

  - HTML5规范提供了一套保护用户隐私的机制。必须先得到用户明确许可，才能获取用户的位置信息。在获取地理位置之前，会询问用户，只有在获得许可之后，才能获取到用户的位置信息。

    javascript 

    ```
    //successCallback:获取成功后会调用,并返回一个position对象，里面包含了地理位置信息 
    //获取失败了会调用，并返回error对象，里面包含了错误信息。 
    //获取当前的地理位置信息 navigator.geolocation.getCurrentPosition(successCallback, errorCallback) 
    //重复的获取当前的地理位置信息 navigator.geolocation.watchPosition(successCallback, errorCallback)
    ```

  - 实例

    <script>

    ```
    	navigator.geolocation.getCurrentPosition(function(position) {
         // 定位成功会调用该方法 
         var latitude = position.coords.latitude; //纬度 
         var longitude = position.coords.longitude; //经度 
         var accuracy = position.coords.accuracy; //精度 
         var altitude = position.coords.altitude //海拔高度 
         console.log(latitude, longitude, accuracy, altitude);
     },
     function(error) {
         // 定位失败会调用该方法 
         // error 是错误信息 4
         alert('错误');
     });
    	  </script>
    ```

  - 在iOS 10中，苹果对webkit定位权限进行了修改，所有定位请求的页面必须是https协议的。

  - 百度地图的用法：

  - 官网：http://lbsyun.baidu.com/

    1. 进入官网 直接找到javascript API
    2. 直接找到示例DEMO，复制源代码
    3. 需要获取密钥 （自己申请，需要一到两个工作日）
    4. 创建应用（填写浏览器端）
    5. 利用密钥去替换script标签里面的“你的密钥”

### web存储

- cookie

  - 传统方式，我们以document.cookie进行存储，但是存储起来特别麻烦，并且，存储大小只有4k，常用来做自动登录，即存储用户的账号和密码信息。每次请求都会带上cookie
  - 在获取cookie内容时，一般需要通过正则或者字符串的方法进行处理，转换成对象，最终得到数据
  - 大小只有4k左右

- window.sessionStorage

  1. 生命周期为关闭浏览器窗口

  2. 不能多窗口下数据可以共享

  3. 大小为5M

  4. 补充：通过跳转可以多窗口共享

     运用场景：在一些单页面（spa）的运用中，进行页面传值的时候比较有用

- window.localStorage

  1. 永久生效，除非手动删除或用代码删除

  2. 可以多窗口共享

  3. 大小为20M

     运用场景：一些不涉及到安全的一些数据（不要太过庞大）都可以存储到本地

- 差异性：（面试经常问）

  - 相同点：都是存储数据，存储在web端，并且都是同源

  - 不同点：
    ​	
    （1）cookie 只有4K 小 并且每一次请求都会带上cookie 体验不好，浪费带宽

    ```
    （2）session和local直接存储在本地，请求不会携带，并且容量比cookie要大的多
    （3）session 是临时会话，当窗口被关闭的时候就清除掉 ，而 local永久存在，cookie有过期时间
    （4）作用域不同，sessionStorage不能在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。
    ```

### 全屏

HTML5规范允许用户自定义网页上任一元素全屏显示。

- requestFullScreen() 开启全屏显示
- cancelFullScreen() 关闭全屏显示

### 文件读取

- 通过FileReader对象我们可以读取本地存储的文件，

- 由于HTML5中我们可以通过为表单元素添加multiple属性，就可以上传多个文件；因此我们通过`<input>`上传文件后得到的是一个FileList对象（伪数组形式）。

- FileReader是一个HTML5新增的对象，用于读取文件。

  var file = document.getElementById("file"); var box = document.getElementById("box");

  ```
  file.addEventListener("change", function () {
  console.dir(file);

  //files:里面存储了所有上传的文件
  //这个data就是我们上传的那个文件
  var data = file.files[0]

  //1. 创建一个文件读取器
  var fr = new FileReader();

  //2. 让文件读取器读取整个文件
  fr.readAsDataURL(data);

  //3. 等待文件读取完
  //onload：文件读取完成后，就会触发
  fr.onload = function () {
      var img = document.createElement("img");
      img.src = fr.result;
      box.innerHTML = "";
      box.appendChild(img);
  }
  });
  ```

## 拖拽

- 在HTML5的规范中，我们可以通过为元素增加draggable="true"来设置此元素是否可以进行拖拽操作，其中图片、链接默认是开启的。
- 根据元素类型不同，需要设置不同的事件监听 
  - 1、拖拽元素 ondrag 应用于拖拽元素，整个拖拽过程都会调用 ondragstart应用于拖拽元素，当拖拽开始时调用 ondragend	应用于拖拽元素，当拖拽结束时调用 //
    - 2、目标元素 ondragover应用于目标元素，当停留在目标元素上时调用 ondrop应用于目标元素，当在目标元素上松开鼠标时调用(浏览器默认不让拖拽，需要组织dragover的默认行为。)