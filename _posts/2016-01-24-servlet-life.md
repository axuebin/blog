---
layout: post
title:  "Servlet学习笔记---Servlet生命周期"
date:   2016-01-24 19:12:54
categories: JavaWeb
tags: Servlet
author: 薛彬
---
* content
{:toc}


这是在学习Servlet的生命周期后留下的笔记，都说理解好生命周期就是理解Servlet的关键，记下来以备不时之需。





### 过程
- 调用init()方法进行初始化。
- 调用service()方法来处理客户端的请求。
- 调用destroy()方法来终止。
- 由JVM得垃圾回收期进行垃圾回收。

这样就算是一个完整的Servlet的生命周期了，当然这只是简单的表示，来看看每个部分。

### init()
- init()方法在第一次创建Servlet时被调用，这是一次性的初始化。
- init()方法常见的格式如下：

```java
public coid init() throws ServletException{
	//初始化代码
} 
```

### service()
- 执行实际任务的主要方法:Servlet容器（Web服务器）调用service()方法来处理客户端的请求，并把格式化的响应写回给客户端。
- 这个方法是由容器调用，不用用户有任何操作。

### doGet()/doPost()
- 这两个方法最常用，用的时候只要覆盖就好了。


### 注意
- 每当有一个servlet请求，就会产生一个新的线程。

### 生命周期图解
![](http://i.imgur.com/FZBpEIR.png)