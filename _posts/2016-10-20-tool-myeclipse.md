---
layout: post
title: web工程在myeclipse中无法显示bin文件夹
keywords: Tool
categories: [Tool]
tags: [Tool]
---
### 问题描述
web工程在myeclipse中无法显示bin文件夹及如何利用build.xml进行打包

### 解决办法
右击工程 --> build path --> Configure Build Path --> 右下方Default output folder
选择路径，一般都是Web/WEB-INF/classes
此时myeclipse中就可以显示bin文件夹，然后将打包工具（build.xml等）放到该文件夹中即可进行打包
