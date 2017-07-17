---
layout: post
title:  "小白学《深入理解es6》--函数"
date:   2017-07-17 13:17:54
categories: 前端
tags: ES6
author: 薛彬
---

* content
{:toc}




## 函数形参的返回值

ECMAScript函数不介意传递来几个参数，即使定义了一个参数，传进来10个参数都是可以的。这是因为参数在函数内部是用一个数组来表示的，也就是说函数接收到的始终是这个数组，即使数组元素为空。

在函数体内，可以通过`arguments`对象来访问这个参数数组，从而获得每一个参数。

函数参数可以分为形参和实参，在JS中，我们可以这样获取两个参数的长度：

```javascript
function foo(a,b){
  var formalParamLen=arguments.callee.length;
  var actualParamLen=arguments.length;
  console.log(formalParamLen);
  console.log(actualParamLen);
};
foo() // 2,0
foo(1) // 2,1
foo(1,2) // 2,2
foo(1,2,3) // 2,3
```

通过执行上面的代码可以发现，`arguments`是实参，在函数内部就可以通过`arguments[0]`等来访问。

但是 ~ `arguments`其实不是一个数组，`Array.isArray(arguments)`的结果是`false`,`typeof arguments`的结果是`object`。

好了，来看看和ES6相关的内容吧~

### 在ECMAScript5中模拟默认参数

通过上文我们知道即使定义了参数也是可以不传递的，所以严谨的做法是是为定义的参数赋予一个默认值。

在ECMAScript5中，往往这样来给参数赋予默认值：

```javascript
function getPrice(name,type){
  type=(typeof type !== "undefined") ? type : "All";
}
```

### ECMAScript6中的默认参数值

在ES6中，就简单了~

```javascript
function getPrice(name,type="All"){
  console.log(name+":"+type);
  console.log(arguments.length)
}
getPrice("apple"); // apple:All
getPrice("apple","China"); // apple:China
```

效果是一样哒~


### 默认参数值对arguments对象的影响

在在ECMAScript5中，比如通过`var param1 = arguments[0]`获取了第一个参数之后对这个`param1`进行修改，则连着`arguments[0]`也会被修改，这是不安全的。

```javascript
function getPrice(name){
  console.log(name); // ES5
  name="ES6";
  console.log(name); //ES6
  console.log(arguments[0]); ES6
}
```

在ES6中，通过赋予默认参数，这种情况就不会发生了：

```javascript
function getPrice(name="ES5"){
  console.log(name); // ES5
  name="ES6";
  console.log(name); //ES6
  console.log(arguments[0]); //undefined
}
```

## 处理无命名参数

### 不定参数

之前说过，可以通过`arguments`来检查函数的实参，在ES6中，通过引入不定参数(rest parmaeters)的特性来解决这个问题。

在函数的参数命名前加三个点（`...`）就表明这是一个不定参数，该参数是一个数组。与`arguments`不同的是，不定参数不包括`...`之前传入的参数。

- 不定参数之后不能有其他参数
- 不能用于对象字面量的setter中

```javascript
function foo(a,...array){
  console.log(arguments.length); // 4
  console.log(array.length); // 3
  console.log(arguments[0]); // 1
  console.log(array[0]); // 2
}
foo(1,2,3,4);
```

不管有没有使用不定参数，`arguments`都是包含所有传入的参数。

## 增强的Function构造函数

允许在`Function`构造函数中使用不定参数：

```javascript
var foo=new Function("...args","return args");
foo(1,2,3) //[1,2,3]
```

## name属性

> 未完待续~


