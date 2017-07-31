---
title: 移动web
date: 2015-03-02 22:57:12
tags: 
-  '移动端开发'
categories: 
-  '前端'
-  '移动端开发'
---

# 移动web

## 点击事件注意点

1. 移动web页面如果不设置视口能不能显示？

```
    早期的移动站并没有专门的技术，基本都是桌面站缩放到移动端显示；可以使用手指捏合缩放也可以使用双击缩放； 双击的时候可能会点到了a标签input按钮。
```

```
	为了判断用户是双击缩放还是真要点击对应的dom元素，就有了一个延迟300毫秒；如果两次点击时间在300毫秒之内 --双击缩放反之，认为我们是点击dom元素。
```

```
    click的延迟问题是历史遗留问题，只在不设置视口的时候会出现；设置了视口属性之后由于 浏览器就知道了这是专门的移动站，那么click的延迟就没有那么久了。
```

```
    虽然还是比touch晚了50毫秒左右，但是这个延迟是完全可以接受的。
```

```
    所以移动端开发时设置了视口之后，click的延迟问题就可以忽略不计了
```

   

## swipe插件

1. 实现上下自由滚动
2. 为了只有滚动，**容器的尺寸要比slide的尺寸要小**，并且**设置slide height:auto**;

## touch事件

1. touchstart

2. touchmove

3. touchend ; 注意该事件中不能获取到位置

4. 获取位置：

   event.touches[0].clientX；
   ​	

   ```
   event.touches[0].clientY;
   ```

------

```
 	
	<!DOCTYPE html>
	<html lang="en">

	<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        html,
        body {
            height: 100%;
            margin: 0;
            padding: 0;
            background-color: yellowgreen;
        }
        
        img {
            transition: all 1s;
        }
    </style>
	</head>

	<body>
    <img src="images/my.gif" alt="">
    <script>
        window.onload = function() {
            document.body.ontouchstart = function(e) {
                // console.log(e);
                // console.log(e.touches[0].pageX);
                var moveX = e.touches[0].pageX - document.querySelector("img").offsetWidth / 2;
                var moveY = e.touches[0].pageY - document.querySelector("img").offsetHeight / 2;
                document.querySelector("img").style.transform = "translate(" + moveX + "px," + moveY + "px)";
            }
            document.body.ontouchmove = function(e) {
                document.querySelector("img").style.transition = "none";
                var moveX = e.touches[0].pageX - document.querySelector("img").offsetWidth / 2;
                var moveY = e.touches[0].pageY - document.querySelector("img").offsetHeight / 2;
                document.querySelector("img").style.transform = "translate(" + moveX + "px," + moveY + "px)";
            }
            document.body.ontouchend = function(e) {
                document.querySelector("img").style.transition = "all 1s";
                var moveX = 0;
                var moveY = 0;
                document.querySelector("img").style.transform = "translate(" + moveX + "px," + moveY + "px)";
            }
        }
    </script>
</body>

</html>
```

注意：在移动端，touch事件原生没有左滑，右滑等，需要自己封装

```
zepto已经封装好。
```

## 左右，长按滑动事件原理

1. 左滑：判断 滑动结束时 移动的 x是 还是负
2. 长按：
   1. 判断 按的时间
   2. 如果移动了 就失效

## rem单位

1. em:默认的大小是继承而来的字体大小,修改自己的font-size即可.

   .em-box{

   ```
     /*  160px 160px
       em = 16px 默认的 font-size
       em 如果自己设置了 font-size 那么会使用自己的大小
       如果 页面中的所有元素 都没有设置 font-size  那么 em的值 都是一样的 只需要调整 页面中的字体大小 就能够实现
      */
     width: 10em;
     height: 10em;
     font-size:20px;
     background-color: hotpink;
   }
   ```

------

1. rem:默认的大小是html的font-size字体大小,修改html的font-size即可.使用rem实现了适配多种不同的屏幕.

   .rem-box{
     /* rem这里的值是 16px

   ```
    页面的 默认字体大小 是 16px
    使用rem作为单位 自己的 字体大小 是可以 随意更改的 并不会影响 rem的值
    rem的值 是 哪里来的
     r rootelement 取决于 html的 font-size
   页面中的元素 使用 rem作为单位 我们只需要调整 谁的大小
     html的font-size
     页面中的 尺寸 需要使用 rem 
        */
     width: 10rem;
     height: 10rem;
     background-color: skyblue;
     font-size:100px;
   }

   ```

   ​

## js动态设置html的font-size改变rem

这一段js需要放在引用文件之前，在载入任何资源之前,保证执行速度

```
  <script type="text/javascript">
    //  屏幕宽度
    // 浏览器中 可视的区域
    // console.log(window.screen.availWidth);
    // 设备的 屏幕宽度 
    // 这两个值 大小不一 桌面端需要注意 移动端 用哪个都可以
    // console.log(window.screen.width);
    // 页面打开时执行
    document.querySelector('html').style.fontSize = window.screen.width / 20 + 'px';
    // 尺寸发生更改   重新计算
    window.onresize = function () {
      document.querySelector('html').style.fontSize = window.screen.width / 20 + 'px';
    }
```

