---
layout: post
title: Node之模块机制
categories : [Node]
tags : [Node]
---
由于JavaScript语言高性能、符合事件驱动、没有历史包袱的特点，所以JavaScript成为了Node的实现语言。同时，Node很容易通过扩展
来构架大型网络应用，每个Node进程都构成这个网络应用中的一个节点，这也是它名字的来源。随着Node的发展，它在不同平台的兼容性越来越好
，在操作系统与Node上层模块系统之间构建了一层平台层架构，即**libuv**。

Node借鉴CommonJS的Modules规范实现了一套非常简单易用的模块系统，NPM对Packages规范的完美支持。CommonJS对模块的定义分为：
**模块引用、模块定义和模块标识**等3个部分。在Node中，模块分为两类：一类是Node提供的模块，叫核心模块；一类是用户编写的模块
，叫文件模块。Node引用模块需要经历三个步骤：

> 路径分析  
> 文件定位  
> 编译执行

在Node的实现中，是基于标识符来进行模块查找的：Node自带的核心模块、相对路径或者绝对路径的文件模块。在查找自定义模块时
（非核心模块）时，沿路径向上逐级递归，直到根目录下的node_modules目录。在文件定位中，CommonJS模块规范允许在标识符中
不包含文件扩展名，此时，Node会按.js、.json、.node的顺序依次补足扩展名。所以，为了提高查找效率，除.js文件以外，在
调用模块时，尽量带上扩展名。

以上是Node的模块规范中最基本的内容，当然，例如核心模块的编写、C/C++扩展模块的编写，算是比较高阶的内容。在不同的平台下
，模块的编译过程区别还是很明显的。在windows下，对C/C++模块通过VC++编译为.dll文件，然后通过dlopen()进行加载；在*nix下
，通过g++/gcc编译为.so文件，然后通过dlopen()加载。

![picture](/images/nodeModules/扩展模块在不同平台的编译和加载过程.png)

具体的实例为：

![picture](/images/nodeModules/require()引入.node文件的过程.png)
