---
layout: post
title: java 变量存储位置
keywords: Java
categories: [Java]
tags: [Java]
---

#### 局部变量
局部变量(基础类型,引用类型)存于栈中,形式参数也属于局部变量

* 基础类型: 引用以及值都保存在栈中
* 引用类型: 引用保存在栈中,值存于堆中

#### 实例变量(定义在类内部方法外的非静态变量)
保存于堆中的对象里

#### 静态变量 
保存于方法区

#### Example

```java

public class Test {
    public static void main(String[] args) {
        int date = 9;
        Test test = new Test();
        test.change(date);
        BirthDate bd = new BirthDate(8, 8, 1996);
    }
    public void change(int i) {
        i = 1024;
    }
}

class BirthDate {
    private int day;
    private int month;
    private int years;

    public BirthDate(int d, int m, int y) {
        this.day = day;
        this.month = month;
        this.years = years;
    }
}

```


对于以上代码,date是局部变量,d,m,y,i都是形参也为局部变量,day,month,years为实例变量,下面分析下main方法执行过程:

* date为局部变量,为基础类型,引用和值都存在栈中
* Test test = new Test();   test为对象引用,存在栈中,对象(new Test())存在堆中
* test.change(date);   方法中,i是局部变量,存在栈中,当change方法执行完毕后,i即会从栈中消失
* BirthDate bd = new BirthDate(8, 8, 1996);  bd为对象引用,存在栈中,对象(new BirthDate())存在堆中,其中d,m,y为形参,是基础类型的局部变量,
故而引用和数据都存在栈中,day,month,years是实例变量,存在堆中的对象(new BirthDate())中,构造方法执行完毕后,d,m,y将从栈中消失。
* main方法执行完毕后,date变量,test,bd引用将从栈中消失,new Test(),new BirthDate()等待垃圾回收器回收

有关java变量存储位置,可结合之前的文章一起看
[http://rmqc0909.github.io/blog/2016/06/java-construction.html](http://rmqc0909.github.io/blog/2016/06/java-construction.html)

