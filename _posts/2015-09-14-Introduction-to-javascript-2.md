---
layout: post
title: JavaScript之垃圾收集机制
categories : [JavaScript]
tags : [JavaScript]
---
上文主要回顾了JavaScript或者每门语言的最基本的知识：关键字、变量、操作符、数据类型以及函数等内容。
本为主要回顾JavaScript的内存机制。

+ 基本类型和引用类型在复制时的区别，基本类型复制后两个空间相互独立，操作互不影响；引用类型复制的是地址（指针），
复制后两个变量引用同一变量。

+ 检测基本数据类型时用typeof，检测引用类型时用instanceof;

        alert(person instanceof Object); // 变量 person 是 Object 吗?  
        alert(colors instanceof Array);// 变量 colors 是 Array 吗?  
        alert(pattern instanceof RegExp);// 变量 pattern 是 RegExp 吗?  

+ JavaScript没有块级作用域，for循环var i;

+ JavaScript 具有自动垃圾收集机制,执行环境会负责管理代码执行过程中使用的内存。原理其实很简单:找出那些不再继续使用的变
量,然后释放其占用的内存。为此,垃圾收集器会按照固定的时间间隔(或代码执行中预定的收集时间),周期性地执行这一操作。

+ 系统分配给Web浏览器的可用内存数量通常要比分配给桌面应用程序的少，目的是防止运行 JavaScript 的网页耗尽全部系统内存而导致系统崩溃。

+ 基本类型值在内存中占据固定大小的空间,因此被保存在栈内存中;引用类型的值是对象,保存在堆内存中。
