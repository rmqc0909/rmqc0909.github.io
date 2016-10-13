---
layout: post
title: Java构造函数
keywords: Java
categories : [Java]
tags : [Java]
---
#### 什么是构造函数
构造函数是一种特殊的函数，用来在对象实例化时初始化对象的成员变量。

#### 构造函数特点

* 构造函数必须与类的名字相同，并且不能有返回值，返回值也不能是void
* 每个类可以有多个构造函数
* 构造函数可以有0个、1个、或1个以上的参数
* 构造函数总是伴随着new操作一起调用，且不能由程序的编写者直接调用，必须要由系统调用。构造函数在对象实例化时会被自动调用，且只运行一次；普通方法是在程序执行到它时被调用，且可以被该对象调用多次
* 构造函数的作用主要是完成对象的初始化工作
* 构造函数不能被覆盖，但是构造函数可以被重载
* 当父类没有提供无参数的构造函数时，子类的构造函数必须显式地调用父类的构造函数；当父类提供了无参数的构造函数时，此时子类的构造函数就可以不显式调用父类的构造函数，在这种情况下编译器会默认调用父类提供的无参数的构造函数；如带有参数的构造函数在不显式的调用父类构造函数时默认调用的是无参数的构造函数

以下是针对最后一个特点的示例代码

```java

class Base2 {
    private int i;
    private int j;

    public Base2(int i, int j) {
        System.out.println ("Base2 i, j constructor");
        this.i = i;
        this.j = j;
    }

    public Base2() {
        System.out.println ("Base2 constructor");
    }

    public Base2(int i) {
        System.out.println ("Base2 i constructor");
        this.i = i;
    }
}
public class Constructors extends Base2{
    public Constructors() {
    }

    public Constructors(int i, int j) {
        //super (i, j);
    }

    public Constructors(int i) {
        super (i);
    }
    public static void main(String[] args) {
        new Constructors ();
        new Constructors (2);
        new Constructors (2, 3);
    }
}

```
运行结果

```java

Base2 constructor
Base2 i constructor
Base2 constructor

```