---
layout: post
title: 委托加载机制
keywords: Java
categories : [Java]
tags : [Java]
---
### ClassLoader层次结构

```java 

public class Test {
    public static void main(String[] args) {
        ClassLoader classLoader = Test.class.getClassLoader();
        System.out.println("Test classloader: " + classLoader);
        ClassLoader classLoader1 = classLoader.getParent();
        System.out.println("Test parent classloader: " + classLoader1);
        ClassLoader classLoader2 = classLoader1.getParent();
        System.out.println("Test grandparent classloader: " + classLoader2);
        ClassLoader classLoader3 = Integer.class.getClassLoader();
        System.out.println("Integer classloader: " + classLoader3);
    }
}

```

#### 输出结果

```java

Test classloader: sun.misc.Launcher$AppClassLoader@42a57993
Test parent classloader: sun.misc.Launcher$ExtClassLoader@28d93b30
Test grandparent classloader: null
Integer classloader: null

```

这里主要涉及三个类加载器

* 根类加载器 (null)
主要加载%JAVA_HOME%\jre\lib下的类,如rt.jar
* 扩展类加载器
主要加载%JAVA_HOME%\lib\ext下的类
* 应用类加载器
主要加载第三方jar包

#### 加载顺序说明

当Test.class要进行加载时，它将会启动应用类加载器进行加载Test类，但是这个应用类加载器不会真正去加载它，而是会调用看是否有父加载器，结果有，是扩展类加载器，扩展类加载器也不会直接去加载，它看自己是否有父加载器，结果它还是有，是根类加载器。

这个时候根类加载器就去加载这个类，可在%JAVA_HOME%\jre\lib下，它找不到Test类，所以它告诉子类加载器，让子类扩展类加载器在%JAVA_HOME%\lib\ext找，找不到，它让它的子类加载器AppClassLoader去找，AppClassLoader找到Test类，加到内存中，并生成Class对象。

由打印结果可以看出，Integer类实际上是由根类加载器加载。
#### 启动类加载器 实际类加载器

上面Test.class中启动类加载器是应用类加载器,实际类加载器也是应用类加载器。

参见
[http://www.cnblogs.com/wang-meng/p/5574071.html](http://www.cnblogs.com/wang-meng/p/5574071.html)