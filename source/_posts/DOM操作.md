---
title: DOM操作
date: 2015-01-13 23:38:04
tags: 
- DOM
categories: 
- js
---

# JS-DOM操作

## 查询

### 标准DOM API

1. document.getElementById
2. document.getElementsByTagName
3. document.getElementsByName
4. document.getElementsByClassName
5. document.querySelector
6. document.querySelectorAll

### 亲属访问

### 属性获取

1. getAttribute 获取某个属性的值
2. getAttibuteNode 获取属性节点

## 增

### 创建

1. document.createElement 创建元素节点
2. document.createTextNode 创建文本节点
3. document.createAttribute 创建属性节点
4. innerHTML 
5. innerText 
6. cloneNode()

### 加入

1. appendChild 追加到结尾处

2. innerHTML

3. insertBefore 将元素插入到某一个元素的前面

   用法：

   ```
   	父元素.insertBefore(新元素，旧元素);
   	//将新元素插入到旧元素之前。
   ```

### 其他方法

1. style的操作
2. setAttribute(属性名，属性值)

## 删除

### 删除元素

1. removeChild 删除元素
2. removeAttributeNode 删除属性

## 修改

### 修改节点

1. 删除节点再加入

### 修改样式

1. style.xxx = vvv;
2. setAttribute

### 修改文本

1. innerHTML
2. innerText
3. 节点操作
4. nodeValue

### 修改属性

1. .XXX=VVV;
2. .setAttibute(属性名，属性值)

## 节点属性

### 常见的节点属性

1. nodeValue 表示节点的值，任何节点都有该属性，但是一般文本节点才使用。

   ![](http://i.imgur.com/ax4YNa0.png)

2. nodeName 表示节点的名字，所有节点都有该属性，但是一般元素节点才使用。元素节点打印的元素名均为大写字母。



1. nodeType 节点类型 js 高程dom节点

   1表示元素节点

   ```
   2表示属性节点
   3表示文本节点
   ```

   以下两个写框架时用的着

   ```
   9表示document
   11表示代码片段 
   ```

## 属性操作

操作属性节点就是属性的增删查改



1. 添加自定义属性，非标准DOM属性

   div.setAttribute('属性名','属性值')

2. .xxx=vvv 添加属性 HTML-DOM

   div.className = 'c'


1. .removeAttribute('');

   注意删除某些只有一个值的单属性是必须完全删除该属性而不能给空值

2. .removeAttributeNode();



