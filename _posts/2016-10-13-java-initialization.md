---
layout: post
title: Java程序初始化顺序
keywords: Java
categories : [Java]
tags : [Java]
---
### Java程序初始化遵循的3个原则
* 静态对象（变量）优先于非静态对象（变量），其中静态对象只初始化一次
* 父类优先于子类进行初始化
* 按照成员变量定义顺序进行初始化，即便成员变量定义散布于方法定义之间，依然在任何方法（包括构造函数）被调用之前先初始化

#### 示例代码
```java
package cn.tk.reuseclazz;

/**
 * Created by xiedan11 on 2016/10/13.
 */
class Base1 {
    static {
        System.out.println ("Base1 static block");
    }
    {
        System.out.println ("Base block");
    }

    public Base1() {
        System.out.println ("Base constructor");
    }
}
public class Derived extends Base1 {
    static {
        System.out.println ("Derived static block");
    }
    {
        System.out.println ("Derived block");
    }

    public Derived() {
        System.out.println ("Derived construction");
    }
    public static void main(String[] args) {
        new Derived ();
    }
}
```

#### 运行结果
```java
Base1 static block
Derived static block
Base block
Base constructor
Derived block
Derived construction
```