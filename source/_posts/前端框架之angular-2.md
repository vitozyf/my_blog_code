---
title: 前端框架之angular-2
date: 2016-05-19 23:12:39
tags: 
- js
- angular 
categories: 
- frame
- angular
---

## 作用域

1. 1个模块中是可以创建多组MVC的。
2. 相互独立的MVC，其$scope是相互独立的。
3. MVC之间是可以相互嵌套的（视图之间相互嵌套），存在父子关系。在子视图中可以访问父视图的数据。
4. 作用域：scope。

## 过滤器

### 内置过滤器

1. 在视图当中显示数据的时候，是原样的显示数据模型的值。

2. 过滤器的作用：在视图显示数据的时候，将要显示的数据进行处理后再显示

3. 如何使用过滤器

   ```{{数据|过滤器的名称：参数...}}```

4. date过滤器

   ```javascript
   对日期进行过滤
   {{time|date}}默认过滤出来的格式是美国人的格式
   {{time|date:"yyyy-MM-dd HH:mm:ss"}}自定义时间过滤器格式
   ```

5. currency货币过滤器

   ```javascript
   {{price|currency}} 默认在前面会加一个$
   {{price|currency："￥"}} 自定义 前面加￥。
   {{price|currency："￥":1}} 指定货币符号和保留小数的位数。再加一个参数1，表示保留一位整数
   ```

6. uppercase转换为大写显示

   ```javascript
   {{info1|uppercase}} 默认全部转换为大写
   ```

7. lowercase转换为小写显示

   ```javascript
   {{info1|lowercase}} 默认全部转换为小写
   ```

8. limitTo 截取数组中指定位数的元素来显示。

   ```javascript
   {{arr|limitTo:3}}显示前面的3个
   {{arr|limitTo:-3}}显示后面的3个
   ```

9. number 处理数字的过滤器

   ```javascript
   指定数字保留的小数的位数
   {{num|number:2}} 保留两位小数
   ```

10. json过滤器

    ```javascript
    将对象转换为字符串
    {{obj|json}} (其实默认情况下如果要显示一个对象，ng会默认调用json过滤器)
    ```

11. orderBy过滤器

    ```javascript
    将数组元素排序后显示，两个参数，第一个参数排序参照，第二个参数是升序（false）或降序(true)
    {{arr|orderBy:"age"}} 将数组中元素以其属性age的值进行排序，默认升序（从小到大）；
    {{arr|orderBy:"age"：true}} 将数组中元素以其属性age的值进行排序，降序排列；
    如果数组的元素时基本数据类型，直接排，默认升序{{arr|orderBy}}；如果要降序，{{arr|orderBy：null:true}}
    ```

12. filter过滤器

    ```javascript
    过滤出数组当中符合条件的元素
    {{stu|filter:{属性1:值1，属性2：值2..} }}  注意，这个参数对象，要和后面的花括号之间有一个空格！！！
    ```

## 自定义服务

1. 第一种方式：模块对象的factory方法
   - 参数1：自定义服务名称
   - 参数2:1个数组[依赖的服务，回调函数callback(通过形参将依赖的别的服务注入)]
     - 当这个服务被注入的时候，这个服务对应的回调函数就会自动执行
     - 这个回调函数的返回值是一个对象或函数
     - 当自定义服务被注入以后，这个服务的名称就代表回调函数返回的东西。
     - 这样就可以写上实现自己功能的代码，什么地方用就注入进去即可。
2. 第二种方式：模块对象的方法，service;这个方法允许我们自定义服务
   - 参数1：自定义服务名称
   - 参数2:1个数组[依赖的服务，回调函数callback(通过形参将依赖的别的服务注入)]
   - 用该方法自定义服务不用return;里面直接用 this.
     - 类似于构造函数创建对象，不用return

### 配置跨域白名单

1. $http支持跨域访问的. 只支持白名单的跨域访问.

2. 需要注意的是,如果进行跨域白名单配置；需要配置 $sceDelegateProvider

   ```
    app.config(["$sceDelegateProvider", function($sceDelegateProvider) {
           $sceDelegateProvider.resourceUrlWhitelist([
               "http://www.baidu.com",
               "http://www.XXX.com",
           ]);
       }])
   ```

## AngularJS的路由Route

1. 用来实现单页面应用。
2. 路由功能并不在angularJS核心文件中，而是以插件的形式存在的。要使用路由功能，必须下载引入（一定要下和angular.js版本匹配的）。
3. 使用路由：（注意：angularJS中的路由的锚链接 默认要以#!开头）
   1. 在创建模块的时候，就要依赖于"ngRoute"模块。
   2. 进行路由的配置；配置的目的：hash值发生变化时做的事情。
      - when()的参数
        - 参数1：代表匹配的路由（锚点值）
        - 参数2：对象，通过键值对的方式指定路由匹配后要做的事情
          - templateUrl:指定要请求的路径，会自动放在页面有指令ng-view的标签下
4. 最基本的使用
   1. 下载angular.route插件（一定要下和angular.js版本匹配的）
   2. 在angular.js后面引入
   3. 创建模块的时候制定依赖"ngRoute"这个模块
   4. 配置路由:设定路由匹配后要做的事情
   5. 请求回来的资源会被放在**ng-view**下面
   6. 默认情况下 ng的锚点值必须要以#!开头
5. 关于路由匹配成功的对象处理的属性
   1. templateUrl:模板的url
   2. redirectTo 跳转到另外一个路由去（重定向）
   3. template：字符串形式的模板
   4. controller:"控制器名"
      - 请求的资源加载到ng-view后，和该控制器名的控制器关联起来了
6. $routeProvider.when()后面可以接一个.otherwise（）执行所有路由不匹配的时候的代码
7. 如果想要匹配没有任何路由的情况，那么匹配的路由就写一个"/"；"/"就代表空路由。

### 路由参数

1. 在路由的后面可以跟queryString类型的参数，并且不影响路由的匹配。
2. 如何拿到跳转路由带过来的参数
   1. 要指定与视图关联的控制器
   2. 创建控制器 $routeParams这个服务就能拿到带过来的参数

### 路由参数2

1. 修改路由规则
   - "/home/:type"
   - 代表匹配到 /home 的路由必须要带参数
   - 带参数的规则： /home/参数
2. 在控制器中直接可以使用$routeParams模块的返回值获取到参数的值
3. 如果希望没有参数也能匹配，那么就在后面加一个? ; "/home/:type?"
4. 多个参数
   1. /home/:type/:name
   2. /home/1/jack