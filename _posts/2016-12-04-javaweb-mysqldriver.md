---
layout: post
title: spring + mybatis 启动tomcat 报错
keywords: spring mybatis 
categories : [JavaWeb]
tags : [JavaWeb]
---

#### 启动tomcat,报如下错误

![picture](/images/javaweb/2016-12-04-mysqldriver.pic)

#### 解决办法

tomcat lib目录下放入数据库驱动包

* mysql: mysql-connector-java-5.1.27.jar
* oracle: ojdbc14.jar

一般找不到类(ClassNotFoundException), 大多是缺少jar包。
对于数据库驱动包,一般都要给tomcat lib目录下也放一份。





