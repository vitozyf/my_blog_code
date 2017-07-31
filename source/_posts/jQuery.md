---
title: jQuery
date: 2015-02-03 22:42:06
tags: 
-  'jquery'
categories: 
-  js
-  'jquery'
---

# jQuery操作1

------

1. ### mouseenter mouseleave事件

   mouseenter mouseleave事件从大盒子到小盒子或小盒子到大盒子过程中屏蔽了事件冒泡（并没有取消冒泡，事件冒泡还是存在）。
   ​	
   <pre>`$("ul li").mouseenter(function (){

   ```
       $(this).css("backgroundColor","red").siblings().css("backgroundColor","");
     })
   ```

     	    $("ul").mouseleave(function (){

   ```
           $(this).children().css("backgroundColor",'');
        })
   ```

     	  }) `</pre>


1. ### hover事件

   </br>
   hover(fn1,fn2)有两个参数，都是回调函数;fn1为鼠标移入时执行的代码，fn2为鼠标移出时执行的代码，在**一定程度上**可以替换mouseenter和mouseleave(*并不是完全可以代替*)

   ```
    $('div').hover(function (){
        $(this).css("backgroundColor","red");
      },function(){
        $(this).css("backgroundColor",'blue');
      });
   ```

------

## 动画函数(jQuery中所有动画都支持时间和回调函数)

1. ### show() hide() toggle()

2. ### 滑入滑出 slide()（改变的是height这个属性值）

   slideDown()	滑入,
   slideUp()	滑出，
   slideToggle()	切换;

   <pre>` var $div = $("div");// 变量本地化
    $("input").eq(0).click(function (){

   ```
         $div.slideDown(2000);
       });`</pre>
   ```


1. ### 淡入淡出 fade（改变的是opacity这个属性值）

   fadeIn()淡入,fadeOut()淡出，fadeTo()淡到，fadeToggle()淡入淡出切换;

   ```
   `$(function () {
         $("#btn").on("click", function () {
             $("div").fadeIn(2000);
         })
         $("#btn1").on("click", function () {
             $("div").fadeOut(2000);
         })
         $("#btn2").on("click", function () {
             $("div").fadeToggle(2000);
         })
         $("#btn3").hover(function () {
             $("div").fadeToggle();
         })
         $("#btn3").click(function () {
             $("div").fadeTo(1000,0.5);
         })
     })`
   ```


1. ### animate动画函数

   支持四个参数：
   params:对象，一组包含作为动画属性和终值的样式属性和及其值的集合

   speed:时间，三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

   easing:运动曲线（不常用）要使用的擦除效果的名称(需要插件支持).默认jQuery提供"linear"（匀速） 和 "swing".

   fn:回调函数，在动画完成时执行的函数，每个元素执行一次。

   <pre>	`// 在一个动画中同时应用三种类型的效果
   $("#go").click(function(){

   ```
   	$("#block").animate({ 
   ```

    			 width: "90%",
    			 height: "100%", 	
    			 fontSize: "10em", 
    			 borderWidth: 10
    	}, 1000 );
   });`</pre>


1. ### 所有的jQuery动画都需要注意，如果想执行当前动画的话，必须先将之前的动画队列清除

   stop()

   作用：停止当前正在执行的动画
   // 第一个参数表示是否清空所有的后续动画
   // 第二个参数表示是否立即执行完当前正在执行的动画

   `$(selector).stop(clearQueue, jumpToEnd);`

   - 解释

     **stop(true, true)   后续动画不会执行，当前动画立即跳到结束的位置**

     **stop(true, false)  后续动画不会执行，当前动画立即停止**

     **stop(false, true)  立即执行后续动画，当前动画立即跳到结束的位置**

     **stop(false, false) 立即执行后续动画，当前动画立即停止**

2. ### 动态创建元素

   - 通过$创建
     - append()在父元素中的最后面追加（会将括号中的元素剪切追加进前面的元素）
     - prepend()在父元素中的最前面追加
     - after()在该元素的后面添加
     - before()在该元素的前面添加
   - 通过.html创建
     - 就是讲原来的innerHTML封装成了html()
     - 没有参数的时候，表示获取标签间的文本内容
     - 有参数的时候表示给标签设置内容

3. ### 克隆节点

   - jQuery中的clone()无论参数是true还是false都表示深度克隆，不但克隆标签本身，还克隆一切子节点。

   - 其参数默认是false，即不克隆时间 

   - *不同点：如果是ture则克隆原来的事件，如果是false则不克隆事件* 

     console.log($("p").clone());

     ```
      $("#btn").on("click", function () {
          $("div").append($("p").clone(false));
      })
     ```

   - 由于字符串具有不可变性，在频繁进行字符串拼接的时候最好将字符串放进数组里，最后再统一用join拼成字符串

4. ### 清空节点

   - $("#div").empty()方法，空的   内容没有了，但是DIV标签本身还存在
   - $("#div").html(""),DIV仍然存在
   - **$("#div").remove();  (最常用)删除的最彻底，连本身标签都不存在了**

5. ### 获取或设置表单的值

   .val();

   没有参数时表示获取表单的值，有参数表示设置表单的值为该参数值。

   ```
      //输入表单值获取焦点和失去焦点时
   	$("input[type='text']").on("focus", function () {
             if($(this).val() == "请输入内容..."){
                 $(this).val("");
             }else{
                 $(this).val( $(this).val());
             }
         }).on("blur", function () {
             if($(this).val() == ""){
                 $(this).val("请输入内容...");
             }else{
                 $(this).val( $(this).val());
             }
         })
   ```

6. ### for in

   可以发现，循环输出的属性并不是按照创建的属性进行排列的。

   ```
   Chrome Opera 的 JavaScript 解析引擎遵循的是新版 ECMA-262 第五版规范。
   因此，使用 for-in 语句遍历对象属性时遍历书序并非属性构建顺序。
   而 IE6 IE7 IE8 Firefox Safari 的 JavaScript 解析引擎遵循的是较老的 ECMA-262 
   第三版规范，属性遍历顺序由属性构建的顺序决定。

   for-in 语句无法保证遍历顺序，应尽量避免编写依赖对象属性顺序的代码。
   如果想顺序遍历一组数据，请使用数组并使用 for 语句遍历。 
   如果想按照定义的次序遍历对象属性，请参考本文针对各浏览器编写特殊代码。
   ```

7. ### 属性操作相关

   .attr() //两个参数时设置属性，一个参数时获取属性

   .removeAttr() //移除属性

   **对于单属性checked\selected\disable等等最好使用.prop()**

   .prop() 原型属性;

8. ### offset

   - jQuery将offset封装成了一个方法，此方法返回一个对象，**用法和原生js不一样**
   - offse()方法返回值有两个属性 left 和 top ，**该值是相对于文档左上角的值（和原生JS的区别），始终是以页面或是body为准，与父元素有无定位 没有关系**。如果要获取离自己最近的定位父元素的距离则用下面的position方法。
   - offsetParent() 找到最近的定位父级元素


   - **其返回值的属性left top 是一个可读写的属性。在设置值的时候，如果元素本身有定位，则以本身设置；如果设置的元素原来没有定位，则会加上一个相对定位。**

9. ### position()方法

   - 返回值为只读属性（不能用该方法设置left top等值）


   - position()方法**不是以边框计算，而是以自身的margin**到里自己最近的定位的父元素的距离，**这是和原生js中offset的区别**。

10. ### width()、height()方法

   - 用于获取浏览器可视区的宽度、高度，number类型

     $(window).width();

     $(window).height();

11. ### On的方式注册事件


1. ### 函数参数组成的伪数组arguments

