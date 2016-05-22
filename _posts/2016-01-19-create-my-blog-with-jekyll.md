---
layout: post
title:  "Github + Jekyll 搭建静态博客"
date:   2016-01-19 14:14:54
categories: 前端
tags: Jekyll Github
author: 薛彬
---

* content
{:toc}


试着用github搭一个博客





## 搭建过程

### 安装Ruby

在ruby官网下载ruby的安装包https://www.ruby-lang.org/en/downloads/ 
安装好后配置环境变量
然后再命令行中输入 ruby -version测试

### 安装RubyGems

这里会出现问题。由于国内的缘故，很用可能用rubygems的官方下载不了，我们得先更换源。

```
gem sources -l 
gem sources --remove https://rubygems.org/
gem sources -a https://ruby.taobao.org/  
gem update --system 
```

### 用RubyGems安装Jekyll

安装jekyll

```
gem install jekyll
```
 
这样就算是把jekyll环境搭好了，很简单是吧。

### 创建博客

我们先创建一个最简单的博客。 
在本地D盘建一个工作区jekyllWorkspace

```
d:
cd jekyllWorkspace
jekyll new Demo
```

此时你可以进入Demo文件夹看看，已经多了很多文件。

```
cd Demo
jekyll serve --watch
```

启动jekyll服务，这时你就可以在浏览器看到效果啦

```
https://localhost:4000/
```

