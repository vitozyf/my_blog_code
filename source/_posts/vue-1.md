---
title: vue-1
date: 2016-10-12 22:34:47
tags: 
- js
- vue
categories: 
- frame
- vue
---

# Vue-总结1

------

## Vue的基本概念

### 基本概念

渐进式 JavaScript 框架，核心功能比较小，如果你要做更强大的功能，就要去集成一些插件和第三方包

核心插件:(全家桶)

- Vue-Router:当触发了页面的超链接之后要渲染出哪个页面(组件)，就得靠路由
- Vuex:全局存取数据(状态管理)

特点:核心插件:(全家桶)

- 已经会了HTML,CSS,JavaScript？即刻阅读指南开始构建应用！
- 简单小巧的核心，渐进式技术栈，足以应付任何规模的应用。
- 20kb min+gzip 运行大小 超快虚拟 DOM 最省心的优化

### 发展历程&未来趋势

- 2014
- 趋势:https://www.awesomes.cn/rank/
- 一个用以创建用户接口(UI)的直观、快速、简洁的 MVVM 框架

---



- Vue的教程:https://cn.vuejs.org/v2/guide/

- 开源的项目:https://segmentfault.com/p/1210000008583242/read?from=timeline

- Vue的专题:https://www.awesomes.cn/subject/vue#应用-框架

- bug解决网站:www.stackoverflow.com

  ​

------

## 指令

1. 作用:

   - 渲染页面(组件)

2. 渲染的过程:

   - Vue实例通过el:app找到Vue要解析的范围，发现html元素中如果有以v-开头的东西，Vue就去解析这些指令，并且给某些html元素填充上值显示
   - Vue指令除了显示组件之外，还提供与用户的交互(比如给某些元素绑定单击事件)

3. 指令:

   - 插值表达式 {{}}

   - v-text&v-html 

     ```
     v-text纯文本显示 v-html会解析字符串中有的标签
     ```

   - v-bind

     ```
     数据绑定 单向数据绑定(模型--->视图)
     什么时候需要? 数据需要动态变化的时候，需要他
     ```

     - 参考:https://cn.vuejs.org/v2/guide/syntax.html#v-bind-缩写

   - v-on

     - 作用:事件绑定，当我们触发了某些事件之后(单击事件)，执行函数，达到和用户交互的目的
     - 事件类型:https://developer.mozilla.org/zh-CN/docs/Web/Events

     ```
     注意:
     	当没有参数的时候，可以省略`()`
     	有参数的时候，如果要传参不能省略`()`
     缩写:
     	v-on:事件类型 = "处理函数"
     	@事件类型="处理函数"
     ```

   - v-model

     - 数据的双向绑定，更改了模型更改了会影响视图，视图更改会影响模型 input radio checkbox
     - Vue.js devtools工具可以看到我们Vue写的项目里面的模型这些东西，但是有一个注意事项，你必须在开发环境中使用才有作用

   - v-if/v-show

     - 作用:条件渲染
     - 参考:https://cn.vuejs.org/v2/guide/conditional.html

     注意：

     ```
     1、v-if / v-show 只接收boolean值
     2、v-if 值为true 就创建 值为false就不创建
     3、v-show 值为true/false都会创建，当值为false是，设置display:none; 值为true 干掉display
     4、v-if/v-else 要贴在一起
     ```

     面试题：

     ```
     v-if&v-show的区别，实际开发中如何选择?
     	一般来说， v-if 有更高的切换开销，而 v-show 有更
     	高的初始渲染开销。因此，如果需要非常频繁地切换，
     	则使用 v-show 较好；如果在运行时条件不太可能改
     	变，则使用 v-if 较好。
     ```

   - v-for

     - 列表渲染
     - 注意点:

     ```
     	当我们遍历每一个item的时候，默认是采取`就地复用`的原则，也就是说得直白一点，下一个item可能复用上一个item，可能会导致两个item指向同一块内存空间，当如果更改我们模型，可能会导致几个地方一起改

     如何解决：
     	v1.x 通过track-by 给遍历到的每一项，设置一个唯一的标识符
     	v2.x 通过key 给遍历到的每一项，设置一个唯一的标识符
     ```

   参考:https://cn.vuejs.org/v2/guide/list.html

4. 参考: https://cn.vuejs.org/v2/api/#指令

------

## 组件

### 概念

- 参考:https://cn.vuejs.org/v2/guide/components.html

1. 功能模块的代码集合
2. 组件可以扩展 HTML 元素，封装可重用的代码。

- 总结:把一些功能代码写在一个组件中，然后需要的时候，导入进来并且使用
- 注意点:

```
1、组件使用起来就有点类似于使用自定义的html标签
2、使用了组件化的开发方式，能将一些零散的代码放在不同的组件中去处理，比如我们项目中有首页，商品列表，购物车，不要把这里面三个功能的代码，都放在id=app的div中，把首页的代码放入到一个组件中，把商品列表放入另外一个组件中，把购物车的代码也放在另外一个组件中，到时候通过自定义标签，在id=app的div中去使用
```

### 实现方式(五种)

- 前四种【了解、特地别是第二种】 + 单文件组件（https://cn.vuejs.org/v2/guide/single-file-components.html）
- 前四种定义组件的方式(登录为例)
  1. 先定义，再注册，最后使用(看代码)
  2. 注册和定义一步到位，最后使用(看代码)
  3. 通过自定义`<template>`标签定义组件，最后使用(看代码)
  4. 通过自定义script标签定义组件，最后使用(看代码)
- 注意点:

```
1、组件要想在id=app的div中使用，必须注册
2、每个组件都需要有一个根元素
3、每个组件内部有自己的data，methods
4、每个组件内部的data是一个函数，并且这个函数必须返回一个对象，这个和根实例要区分
5、Vue文档中，定义组件就是使用第二种方式
6、第三种、第四种是对我们第二种中template的简化
```

------

## 过滤器

- 作用:对服务器返回的数据进行过滤处理，将它变成符合展示要求的数据

- 分类:

  - 私有过滤器

    - 是和每个Vue实例相关的，在实例的filters中先定义好，函数

      ```javascript
      filters:{
        toUpperCase:function(input){
          return input.toUpperCase()
        }
      }
      ```

    - 调用过滤器的方法，进行过滤，使用`|`

  - 全局过滤器

    - 注意点:

      ```
      1、过滤器中都是一些函数，并且这些函数必须要有返回值
      2、过滤器的函数的第一个参数，就是`|`前面，我们在调用函数的时候，只需要从第二个参数传起
      ```

------