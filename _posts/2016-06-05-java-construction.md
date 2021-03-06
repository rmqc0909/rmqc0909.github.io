---
layout: post
title: jvm结构图
keywords: Java
categories: [Java]
tags: [Java]
---
## 先来看一张图
下图主要描述了jvm的各个工作区

![picture](/images/java/runtime data area.png)

## 接下来对每个区域进行简要说明

### method area(permanent generation)
类型信息和类的静态变量都存储在方法区。方法区对于每个类存储了以下数据：类及其父类的全限定名(如：java.util.Date),类的类型,访问修饰符,实现的接口的全限定名的列表,常量池：(存储了字符串，final变量值，类名，方法名常量),字段信息,方法信息,静态变量,classloader引用,class引用

### heap
堆是jvm所管理的内存中最大的一块，是被所有java线程所共享的，不是线程安全的，在jvm启动时被创建。
堆用于存储对象实例以及数组值。

### java stack
java栈主要任务是存储方法参数，局部变量，中间运算结果，java栈总是与线程关联在一起，每创建一个线程，jvm就会为该线程创建对应的java栈，java栈包含很多栈帧，每个栈帧是与方法关联起来的，每运行一个方法就创建一个栈帧。java栈栈顶的栈帧就是当前正在执行的方法。
java栈与线程相对应，java栈数据不是线程共有的，不需要关心数据一致性，也不会存在同步锁问题。
分为三部分：局部变量区,操作数栈,栈数据区。
java虚拟机规范中，对该区域规定了两种异常：如果线程请求的栈深度大于虚拟机所允许的深度，将抛出StackOverFlowError;如果虚拟机可以动态扩展，若扩展时无法申请到足够内存，会抛出OutOfMemoryError异常。

### program counter register
一种数据结构，保存当前正在执行的程序的内存地址。


### classloader
类加载子系统负责加载编译好的.class字节码文件，并装入内存，使jvm可以实例化或者以其他方式使用加载后的类。

支持运行时的动态加载，优点有，节省内存空间，灵活的从网络上加载类，通过命名空间的分隔来实现类的隔离，增强了整个系统的安全性。










