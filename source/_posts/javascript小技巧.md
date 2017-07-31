---
title: javascript小技巧
date: 2014-11-21 15:24:30
tags: 
- js
categories: 
- js
---

1.将arguments转化为数组
函数中的预定义变量arguments并非一个真正的数组，而是一个类似数组的对象。 
它具有length属性，但是没有slice, push, sort等函数，那么如何使arguments具有这些数组才有的函数呢？ 
也就是说如何使arguments变成一个真正的数组呢？

2.

3数组中的最大值

var arr = [2, 3, 45, 12, 8];

Math.max.apply(null, arr);// 45

4.修改arguments

function add() { 

​       Array.prototype.push.call(arguments, 123);

 //因为arguments不是数组，是类数组，故需要调用数组方法

​       return arguments; 

 } 

add(100); // [100,123]

 

/***1-4   数组操作**/

 

5.判断一个变量是否为undefined  

​      typeof(name2) === ‘undefined’;// true

6.私有变量

 var person =(function() {

​    var _name='1000';

​    return {

​        getName:function() {   return _name || '2000';   }   

​    }

 })();   

person.getName(); // "1000"   

typeof(person._name); // "undefined"

 

7.JavaScript没有块级上下文（Scope）.即函数才是作用域

 for(var i = 0; i < 2; i ++) { } 

i;  // 2

8.If 中的假：null, undefined, NaN, 0, ‘’, false

9.0.1+0.2 != 0.3
 JavaScript将小数作为浮点数对待，所以可能会产生一些四舍五入的错误，比如：

​             0.1 + 0.2; // 0.30000000000000004

你可以通过toFixed方法指定四舍五入的小数位数：

​            (0.1 + 0.2).toFixed(); // "0"

​            (0.1 + 0.2).toFixed(1); // "0.3"      

1. encodeURI和encodeURIComponent  

window.encodeURI函数用来编码一个URL，但是不对这些编码：“:”, “/”, “;”, “?”. 
window.encodeURIComponent则会对上述字符进行编码。
我们通过一个例子来说明：

​       'index.jsp?page='+encodeURI('/page/home.jsp');  // "index.jsp?page=/page/home.jsp"

​       'index.jsp?page='+encodeURIComponent('/page/home.jsp');  // "index.jsp?page=%2Fpage%2Fhome.jsp"

因此，在对URL进行编码时我们经常会选择 encodeURIComponent。 

11.table.innerHTML在IE的table下是只读属性

<table id="table1"> </table>

​           // works well in Firefox, but fail to work in IE

document.getElementById('table1').innerHTML = "<tr><td>Hello</td><td>World!</td></tr>";

应该：

document.getElementById('table1').innerHTML = "<table><tr><td>Hello</td><td>World!</td></tr></table>";

 

12.Boolean 和 new Boolean

我们可以把Boolean看做是一个函数，用来产生Boolean类型的值（Literal）：

​            Boolean(false) === false; // true 

​            Boolean('') === false; // true       

所以，Boolean(0)和!!0是等价的。 
我们也可以把Boolean看做是一个构造函数，通过new来创建一个Boolean类型的对象：

​            new Boolean(false) === false; // false 

​            new Boolean(false) == false; // true 

​            typeof(new Boolean(false)); // "object" 

​            typeof(Boolean(false)); // "boolean"

13.一元操作符 +在JavaScript中，我们可以在字符串之前使用一元操作符“+”。这将会把字符串转化为数字，如果转化失败则返回NaN。【原理未知】

​            2 + '1'; // "21"

​            2 + ( +'1'); // 3     

如果把 + 用在非字符串的前面，将按照如下顺序进行尝试转化：

1 调用valueOf()

2 调用toString()

3 转化为数字

​            +new Date; // 1242616452016

​            +new Date === new Date().getTime(); // true

​            +new Date() === Number(new Date) // true