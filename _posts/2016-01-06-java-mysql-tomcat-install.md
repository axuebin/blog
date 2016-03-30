---
layout: post
title:  "mysql、tomcat、java安装配置"
date:   2016-01-06 18:54:00
categories: Other
tags: Java Mysql Tomcat
---
* content
{:toc}

## java 

也就是配置jre和jdk

### 下载JDK
http://www.oracle.com/technetwork/java/javase/downloads/index.html

### 配置环境变量
 - **JAVA_HOME**: C:\Program Files\Java\jdk1.8.0_65 //就是JDK的安装目录
 - **CLASSNAME**: .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; 
 - **Path**: %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

### 测试
cmd中输入java -version , java , javac 等命令

-------------------

## Tomcat

### 下载Apache Tomcat
https://tomcat.apache.org/download-80.cgi 

### 配置环境变量
 - **CATALINA_BASE**: D:\apache-tomcat-8.0.30   //Tomcat的安装目录
 - **CATALINA_HOME**: D:\apache-tomcat-8.0.30  //Tomcat的安装目录
 - **Path**: %CATALINA_HOME%\lib;%CATALINA_HOME%\bin

### 测试
在bin中找到startup，双击，在浏览器中输入 localhost:8080,有页面就说明配置成功。

### 配置用户
编辑conf/tomcat-users.xml, 在最后加上

	<role rolename="admin-gui"/>
	<user password="123456aaa" roles="admin-gui,manager-script,admin" username="xb"/>

-------------------

## Mysql

### 下载Mysql
https://dev.mysql.com/downloads/mysql/

### 配置环境变量
 - **Path**: D:\mysql-5.7.10-winx64\bin;     //安装目录的bin目录

### 添加my.ini文件

	[mysqld]

	#绑定IPv4和3306端口
	bind-address = 0.0.0.0
	port = 3306

	# 设置mysql的安装目录
	basedir=D:\mysql-5.7.10-winx64

	# 设置mysql数据库的数据的存放目录
	datadir=D:\mysql-5.7.10-winx64\data  // data文件在mysql5.7之后没有了

	# 允许最大连接数
	max_connections=200

### 安装mysql
cmd（管理员） 进入bin目录，运行 mysqld -install, 提示success即成功安装。


