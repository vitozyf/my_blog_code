---
title: Angular在实际应用中的优缺点
date: 2016-06-03 21:54:28
tags: 
- js
- angular 
categories: 
- frame
- angular
---

## 遇到的坑

与传统JQ思维方式不同，会出现很多理解上面的冲突。谈一个我遇到过的坑。

当用户操作某个input，改变了某个值，这个值需要在另一个地方显示，所以在angular绑定中，改变input的同时，另一个地方的显示也会跟着变。那么问题来了，当我不需要另一个地方的显示跟着变，而是需要用户点击某个buttom之后再变，那我就需要两个变量来存储这个值。事实上这只是同一个值，只是我不需要立马显示在页面上罢了。

正常思维中，这个值只是一个值，我什么时候需要显示，是JS的事情，所以我只需要一个变量来存。在Angular中，由于我要延迟显示，我需要一个变量来做缓存，等到需要显示的时候再去显示。

页面绑定非常厉害，厉害到需求发生变化的时候，你会发现各个数据全都是绑定着的，牵一发动全身，然后就要进行解绑、绑定新数据、解绑后是否会引起其他地方的bug等诸多问题。

如果与backbone进行比较，页面渲染时的数据交给模板插件，页面渲染结束后的与用户进行交互方面的逻辑交给JS，我可以在不改变model的情况下改变页面上的内容，更灵活。

当然在很多人眼里，这些只是小瑕疵，无法掩盖它的优势。成也绑定，败也绑定。Angular的优势，很多方面backbone也有，如模块化、MVC分离、SPA(single page application)，在交互方面，backbone更加灵活。当然在我眼里，拼了命地绑定绑定，让我觉得HTML和JS的耦合性太高，写起代码来很累。

## 优点：

1. 模板功能强大丰富，并且是声明式的，自带了丰富的Angular指令；

2. 是一个比较完善的前端MV*框架，包含模板，数据双向绑定，路由，模块化，服务，过滤器，依赖注入等所有功能；

3. 自定义Directive，比jQuery插件还灵活，但是需要深入了解Directive的一些特性，简单的封装容易，复杂一点官方没有提供详细的介绍文档，我们可以通过阅读源代码来找到某些我们需要的东西，如：在directive使用 $parse；

4. ng模块化比较大胆的引入了Java的一些东西（依赖注入），能够很容易的写出可复用的代码，对于敏捷开发的团队来说非常有帮助，我们的项目从上线到目前，UI变化很大，在摸索中迭代产品，但是js的代码基本上很少改动。

5. 补充：Angular支持单元测试和e2e-testing。

6. 感觉AngularJS最大的优点

   - 改变操作dom的方式

     将传统的JQuery的先选择元素，在操作的方式改变成了直接对于元素本身的操作。
     这依赖于强大的Html Parser的能力和directive灵活。

   - 后端MVC前端化

     是的，[http://ASP.net**](https://link.zhihu.com/?target=http%3A//ASP.net) MVC， strucs的很多机制，完全可以用AngularJS替代有没有？。。。

   - 数据操作

     依赖于良好的后端restful接口的配合，完全的变成了早些年pb这样的数据集成化开发有没有？

## 缺点：

1. 验证功能错误信息显示比较薄弱，需要写很多模板标签，没有jQuery Validate方便，所以我们自己封装了验证的错误信息提示，详细参考 [why520crazy/w5c-validator-angular · GitHub**](https://link.zhihu.com/?target=https%3A//github.com/why520crazy/w5c-validator-angular) ；
2. ngView只能有一个，不能嵌套多个视图，虽然有 [angular-ui/ui-router · GitHub**](https://link.zhihu.com/?target=https%3A//github.com/angular-ui/ui-router) 解决，但是貌似ui-router 对于URL的控制不是很灵活，必须是嵌套式的（也许我没有深入了解或者新版本有改进）；
3. 对于特别复杂的应用场景，貌似性能有点问题，特别是在Windows下使用chrome浏览器，不知道是内存泄漏了还是什么其他问题，没有找到好的解决方案，奇怪的是在IE10下反而很快，对此还在观察中；
4. 这次从1.0.X升级到1.2.X，貌似有比较大的调整，没有完美兼容低版本，升级之后可能会导致一个兼容性的BUG，具体详细信息参考官方文档 [AngularJS**](https://link.zhihu.com/?target=http%3A//docs.angularjs.org/guide/migration) ，对应的中文版本：[Angular 1.0到1.2 迁移指南**](https://link.zhihu.com/?target=http%3A//ngnice.com/docs/guide/migration)
5. ng提倡在控制器里面不要有操作DOM的代码，对于一些jQuery 插件的使用，如果想不破坏代码的整洁性，需要写一些directive去封装插件，但是现在有很多插件的版本已经支持Angular了，如：[jQuery File Upload Demo**](https://link.zhihu.com/?target=http%3A//blueimp.github.io/jQuery-File-Upload/)
6. Angular 太笨重了，没有让用户选择一个轻量级的版本，当然1.2.X后，Angular也在做一些更改，比如把route，animate等模块独立出去，让用户自己去选择。