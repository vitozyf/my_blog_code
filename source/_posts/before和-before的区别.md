---
title: ':before和::before的区别'
date: 2015-05-10 22:37:45
tags: 
- css
- "伪类"
- "伪元素"
categories: 
- css
---

在一次项目中，有一次要用到::selection伪元素，然后开发同学问我，CSS中一个冒号和两个冒号有神马区别？



这好像真的是个问题，或许很多前端同学对此都有疑惑，查了些资料，证实了下两个符号的区别，简而言之：**单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素**。



[W3C关于CSS3选择器的规范](http://www.w3.org/TR/2005/WD-css3-selectors-20051215/#pseudo-elements)中有一段描述：

```
A pseudo-element is made of two colons (::) followed by the name of the pseudo-element.
This :: notation is introduced by the current document in order to establish a discrimination between pseudo-classes and pseudo-elements. For compatibility with existing style sheets, user agents must also accept the previous one-colon notation for pseudo-elements introduced in CSS levels 1 and 2 (namely, :first-line, :first-letter, :before and :after). This compatibility is not allowed for the new pseudo-elements introduced in CSS level 3.
```



简单翻译一下，大意就是，伪元素由双冒号和伪元素名称组成。双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存 在的伪元素写法，比如:first-line、:first-letter、:before、:after等，而新的在CSS3中引入的伪元素则**不允许**再支持旧的单冒号的写法。



那么现在就可以完整的回答标题中的问题了，对于CSS2之前已有的伪元素，比如:before，单冒号和双冒号的写法::before**作用是一样的**。



所以，如果你的网站**只需要**兼容webkit、firefox、opera等浏览器，建议对于伪元素采用双冒号的写法，如果不得不兼容IE浏览器，还是用CSS2的单冒号写法比较安全。