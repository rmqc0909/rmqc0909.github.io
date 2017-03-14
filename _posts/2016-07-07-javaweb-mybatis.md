---
layout: post
title: mybatis错误分析
keywords: Mybatis
categories: [JavaWeb]
tags: [JavaWeb]
---
### 错误描述
项目采用**mybatis + spring**时，更新sql时，抛出如下错误：

![picture](/images/javaweb/2016-07-07-mybatis.png)

### 解决方法

mybatis插入空值时，需要指定jdbcType
将入参格式改为：#{mobile, jdbcType = VARCHAR}
