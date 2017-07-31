---
title: jQuery2
date: 2015-02-05 21:30:38
tags: 
- 'jquery'
categories: 
- js
- 'jquery'
---

# jQuery2

## 

1. ### scrollTop()、scrollLeft()、scroll()

   scrollTop()、scrollLeft()是可读写方法，既可以获取值也可以设置值。

   ```
   <script>
     $(function(){
         // 原生JS当中是把事件注册给了window  window.scroll = function(){}
       // scrollLeft()  scrollTop() 封装成了可读写的方法
        $(window).scroll(function (){
             console.log($(window).scrollTop());
             console.log($(window).scrollLeft());
        })
     })
   </script>
   ```

2. ### jQuery中的简单事件绑定 .事件名称

   jQuery中的简单事件绑定相当于把js中的on注册事件分装成了对应的方法，而且进行了优化。对于同一事件源，注册多个相同事件的话，会依次执行事件，不会覆盖原来的事件。

   - **优点：可以给同一事件源注册多个事件，不会覆盖。**

3. ### （了解）bind注册事件（1.7以后的jQuery全部被on代替）

   好处是可以给同一个事件源绑定多个相同的事件（多个事件的事件处理程序一致），但不能实现事件委托。

   - 缺点：要绑定事件的元素必须存在在文档中;不能实现事件委托。

     // 好处是，可以给同一个事件源，绑定多个相同的事件(多个事件的事件处理程序一致)

     ```
     $('input').bind('click mouseenter',function (){
       alert('愿岁月静好');
     });
     ```

4. ### （了解）delegate注册事件

   和bind基本一样，但可以实现事件委托。

   - 相对于bind的优点：支持给动态创建的元素注册事件。

     <script>

     ```
        $(function(){
        //$('input').bind('click mouseenter',function(){})
        //$('ul').delegate('li','click',function (){
        //  alert('愿岁月静好');
        //})
         $('div').delegate('p','click mouseenter',function (){
           alert('愿岁月静好');
         });
         // 支持给动态创建的元素注册事件
       })
     ```

      	</script>

   delegate 只能通过子元素触发事件，自己本身不能触发

5. ### (了解)bind 和 dalegate 的区别

   delegate支持动态创建的元素的时间注册，bind不支持

6. ### (重点)on的方式注册事件

   - on的方式具有前面所有注册事件方式的优点

     jQuery1.7版本后，jQuery用on统一了所有的事件处理的方法

     ```
     作用：给匹配的元素绑定事件，包括了上面所有绑定事件方式的优点
     ```

     ```
     语法：
     // 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
     // 第二个参数：selector, 执行事件的后代元素
     // 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用
     // 第四个参数：handler，事件处理函数
     $(selector).on(events[,selector][,data],handler);

     // 表示给$(selector)绑定事件，当必须是它的内部元素span才能执行这个事件
     $(selector).on("click","span", function() {});

     // 绑定多个事件
     // 表示给$(selector)匹配的元素绑定单击和鼠标进入事件
     $(selector).on("click mouseenter", function(){ });
     ```

   第三个参数演示：
   ​		

   ```
   			<script>
           $(function () {
   //            $("input").on("click", function () {
   //                alert(123);
   //            })
   			//采用event.date存储注册时传递的数据，不会随变量变化而改变
   //            var num = 10;
   //            $("input").on("click", num,function (e) {
   //                alert(e.data);
   //            })
   //            var num = 20;
   //            $("input").on("mouseenter", num,function () {
   //                alert(num);
   //            })
   			 //当然，也可以传对象进来
               var num = {
                   name:"zs"
               };
               $("input").on("click", num,function (e) {
                   alert(e.data.name);
               })
           })
       </script>
   ```

7. ### 事件解绑

   - unbind() 方式 和 undelegate() 方式

     作用：解绑 bind方式绑定的事件

     ```
     $(selector).unbind(); //解绑所有的事件
     $(selector).unbind("click"); //解绑指定的事件

     作用：解绑delegate方式绑定的事件
     $( selector ).undelegate(); //解绑所有的delegate事件
     $( selector).undelegate( "click" ); //解绑所有的click事件
     ```

   - off解绑on方式绑定的事件（重点）

     // 解绑匹配元素的所有事件

     ```
     $(selector).off();
     // 解绑匹配元素的所有click事件
     $(selector).off("click");
     // 解绑所有代理的click事件，元素本身的事件不会被解绑 
     $(selector).off( "click", "**" ); 
     ```

8. ### 阻止默认行为

   - return false;	
   - event.preventDefault()

9. ### 阻止冒泡

   - e.stopPropagation()

   jQuery中使用这一个即可，没有兼容性，将兼容性的方法都封装在该方法中了

   （e.cancelBubble = true是原生JS中IE浏览器支持的方式）

10. ### 事件对象中的几个属性

   this 始终指代当前对象，正在执行事件处理程序的事件源。

   e.target 始终表示最原始的事件源，没有兼容性问题。

   e.currentTarget 和this一样。

   e.delegateTarget 也和this一样。

11. ### 事件对象中的坐标

    e.screenX / Y（浏览器）

    e.clientX / Y （可视区）

    e.pageX / Y（页面）

    没有兼容性问题

12. ### 触发器

    $(selector).click(); // 简单事件触发，触发 click事件

    $(selector).trigger("click"); // trigger方法触发事件

    $(selector).triggerHandler("focus"); // triggerHandler触发 事件响应方法，不触发浏览器行为 比如:文本框获得焦点的默认行为闪烁光标。

    ```
    <script>
          $(function(){
               $("input:eq(1)").on("click",function (){
                      alert(123);
               })
            // 是单击第一个按钮的时候，来触发第二个按钮的单击事件
            $("input:eq(0)").on("click",function (){
    //               $("input:eq(1)").click();
                   //$("input:eq				(1)").trigger("click"); // 写上参数对应的事件名称
    //              $("input:eq(1)").triggerHandler('click');
              
    //          $("input:eq(2)").trigger('focus');
              $("input:eq(2)").triggerHandler('focus'); //  触发事件的时候，不会引发默认行为
              // 输入框的焦点获取到之后，闪烁的光标是一个默认行为
            })
            
            $("input:eq(2)").on('focus',function (){
                   $(this).next().text('输入框的焦点获取了');
            })
          })
      </script>
    ```

13. ### each方法

    **each是jQuery中的方法，一定要用jQuery对象来调用！！！**

    **用来遍历jQuery对象**

    （js中的foreach用来遍历数组）

```
- 有了隐式迭代，为什么还要使用each函数遍历？
```

```
		大部分情况下是不需要使用each方法的，因为jQuery的隐式迭代特性。
		如果要对每个元素做不同的处理，这时候就用到了each方法
		
		作用：遍历jQuery对象集合，为每个匹配的元素执行一个函数
		
		// 参数一表示当前元素在所有匹配元素中的索引号
		// 参数二表示当前元素（DOM对象）
		$(selector).each(function(index, element){});
		
		$.each(object, function(k, v) {});

**第二种用法，也可以遍历数组和对象**

		 <script>
	      $(function(){
	           // 是用来遍历jQuery对象 和数组
	        // 慢慢变成正常显示的一个效果
	//        $("ul li").css("opa")
	//        $("ul li").each(function (index,ele){
	//          // ele是DOM对象
	////               console.log(index+"====="+ele.innerHTML);
	//           $(ele).css("opacity",(index+1)/10)
	//        })
	        
	        // forEach   是用来遍历数组的
	        // each 是jQuery中的方法，一定要用jQuery对象来调用
	        var nums = [10,20,30,40,50,60,70,80];
	//        nums.forEach(function (item,index){
	//               console.log(index+"===="+item);
	//        })
	        var obj = {
	          name:"张三",
	          age: 20,
	          sex:"男"
	        }
	//        $.each(nums,function (index,ele){
	//               console.log(index+"======="+ele);
	//        })
	        $.each(obj,function (index,ele){
	          console.log(index+"======="+ele);
	        })
	      })
	  </script>
```

1. ### end()方法

   回到最近的一个"破坏性"操作之前。即，将匹配的元素列表变为前一次的状态。

   如果之前没有破坏性操作，则返回一个空集。所谓的"破坏性"就是指任何改变所匹配的jQuery元素的操作。这包括在 Traversing 中任何返回一个jQuery对象的函数--'add', 'andSelf', 'children', 'filter', 'find', 'map', 'next', 'nextAll', 'not', 'parent', 'parents', 'prev', 'prevAll', 'siblings' and 'slice'--再加上 Manipulation 中的 'clone'。

2. ### 多库共存的解决方式

   此处多库共存指的是：jQuery占用了$ 和jQuery这两个变量。当在同一个页面中引用了jQuery这个js库，
   并且引用的其他库（或者其他版本的jQuery库）中也用到了$或者jQuery这两个变量，那么，
   要保证每个库都能正常使用，这时候就有了多库共存的问题。

   $.fn.jquery 测试jquery版本

   $.noConflict() 让出$符号的控制权，有返回值，可以传给其他变量

   var  itcast = $.noConflict(),此时itcast用法和$一模一样。

   ```
   	<script src="js/jquery-1.10.2.js"></script>
   	<script src="js/jquery-1.12.2.js"></script>
   	<script src="js/jquery-2.2.2.js"></script>
   	//如上多库共存，第一次使用$.noConflict()最后一个js库会让出$控制权，再次使用$.noConflict()倒数第二个库会让出$控制权。。。
   ```

```
		//让出$的控制权
		console.log($.fn.jquery);
		var itcast= $.noConflict();
		console.log($.fn.jquery);

		//如果想再用$，可以如下使用自调用函数，将让出来的控制权赋给变量itcast后再作为参数传到自调用函数，即可在自调用函数内部使用$
		(function($){
		  $("input").on("click",function (){
		         alert(123456789);
		  });
		})(itcast);
```



1. ### 插件

   所谓插件就是依赖于某个库文件，对该库文件其中某些个方法，进行功能的完善。

   简单引用插件的步骤：

   ```
   1>引入jquery文件包
   ```

   ```
   2>引入插件文件
   ```

   ```
   3>调用方法（仍然是jquery方法，插件只是完善某些方法）
   ```

   正常后台取数据调用插件

   ```
   1>引入html静态文件
   ```

   ```
   2>引入css样式文件
   ```

   ```
   3>引入jQuery文件
   ```

   ```
   4>引入插件文件
   ```

   ```
   5>调用插件对应方法
   ```

   - 背景插件

     背景颜色最好用十六进制表示

2. ### 制作插件

   如何创建jQuery插件：
   `http://learn.jquery.com/plugins/basic-plugin-creation/`

   全局jQuery函数扩展方法

   $.pluginName = function() {};

   $.pluginName();

   jQuery对象扩展方法

   $.fn.pluginName = function() {};

   $(selector).pluginName();