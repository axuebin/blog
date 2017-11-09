---
layout: post
title:  "JavaScript基础心法——数组（没写完。。最近有点懒。。）"
date:   2017-11-09 15:08:00
categories: 前端
tags: JavaScript
author: 薛彬
---

* content
{:toc}

在JavaScript的世界中，除了 `Object` 之外， `Array` 恐怕是最常用的类型了。




## 如何创建数组

现在创建数组一般有三种方式：

- 构造函数
- 数组字面量
- ES6新增的方法

先看看第一种方式。因为 `Array` 也是一种对象，所以也可以用构造函数的方式来创建一个数组，比如这样：

```javascript
const arr = new Array(); // 创建一个空数组
const arr = new Array(5); // 创建一个长度为5的空数组
const arr = new Array(1,2,3,4,5); // 创建一个[1,2,3,4,5]数组
```

当然，我们可以简单一点，直接用数组字面量表示法，也就是直接写出一个数组：

```javascript
const arr = []; // 创建一个空数组
const arr = [5]; // 创建一个长度为1数值为5的数组
const arr = [1,2,3,4,5]; // 创建一个[1,2,3,4,5]数组
```

这样创建数组应该是最常用到，简单直观。

还有一种方式是ES6中新增的方式，我们观察一下通过构造函数创建数组，当我们使用 `new Array(5)` ，也就是只传递一个值时，它创建的是一个长度为这个值的数组，这点会让人疑惑。

有的人可能是想创建一个 `[5]`，但是意外地创建了一个**长度为5**的空数组，这就尴尬了。

所以，引入了一个新的方法 `Array.of()` 来创建数组。

```javascript
const arr = Array.of(); // 创建一个空数组
const arr = Array.of(5); // 创建一个长度为1数值为5的数组
const arr = Array.of(1,2,3,4,5); // 创建一个[1,2,3,4,5]数组
```

是不是很完美。

有的人说，这个是个 `ES6` 方法，不用 `ES6` 怎么办呢。简单啊，我们自己做一个 `Array.of()`：

```javascript
if(!Array.of){
  Array.of = function(){
    return Array.prototype.slice.call(arguments);
  }
}
``` 

`arguments` 是传递到函数中的所有参数，这会是一个类数组对象， `slice` 方法等会儿会介绍到，现在只需要知道它能复制传递进去的那个数组。

## 数组的长度

- `length` 属性表示数组的长度
- 当数组有空元素的时候，`length` 属性不一定表示数组中定义值的个数
- 通过 `arr.length` 设置数组长度有可能截断数组

## 检测数组

说到类型的判断，第一个想法是 `typeof` 吧，但是遗憾的是，`typeof [1,2,3]` 的结果是 `object`。

目前可以判断是否是数组一般有以下几种方法：

```javascript
const arr = [1,2,3,4,5];
console.log(arr instanceof Array); // true
console.log(arr.constructor == Array); // true
console.log(Object.prototype.toString.call(arr)=='[object Array]'); // true
console.log(Array.isArray(arr)); // true
```

`Array.isArray()` 是 `ES6` 的新方法，如果需要兼容旧浏览器，可以这样：

```javascript
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

## 数组的常用方法

### Array.from()

`ES6` 。

这是一个很实用的方法。我们知道除了数组之外，还存在一种类数组类型，比如 `document.querySelectorAll` 返回的 `NodeList`，在表面上和数组长得一模一样，但是却没有类似 `map`、`foreach` 这样数组有的方法，我们常常会这样做：

```javascript
var nodeList = document.querySelectorAll('div');
Array.prototype.map.call(nodeList,function(value){
  console.log(value);
})
```

或者是通过 `Array.prototype.slice.call(nodeList);` 浅拷贝一下。

这样一串的代码看起来就不优雅，特别是看到 `prototype` 这个东西，总感觉这东西应该被封装起来。

我们现在可以这样做：

```javascript
const nodeList = document.querySelectorAll('div');
const nodeArr = Array.from(nodeList);
nodeArray.map(value => console.log(value));
```

是不是很爽？

还有一种更酷的方式：

```javascript
const nodeList = document.querySelectorAll('div');
[...nodeArray].map(value => console.log(value));
```

这是用了 `ES6` 的展开运算符来完成数组的拷贝 ~

**值得一提的是，`Array.from()` 可以用在 `String`、`Set`、`Map`等各种类数组对象或者可迭代对象。**

```javascript
console.log(Array.from('axuebin'))l // ['a','x','u','e','b','i','n'];
function foo(){
  console.log(Array.from(arguments)); // 转换函数传递参数的 arguments 类数组
}
```