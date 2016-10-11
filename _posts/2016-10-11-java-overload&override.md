---
layout: post
title: 多态机制--重载与覆盖
keywords: Java
categories : [Java]
tags : [Java]
---
### java的多态机制
java提供了编译时多态和运行时多态两种机制。编译时多态是通过方法的重载实现，运行时多态是通过方法覆盖（子类方法覆盖父类方法）实现。

#### 重载

重载是指在一个类中定义了多个同名的方法，这些方法或有不同的参数个数，或有不同的参数类型，或有不同的参数顺序。

* 重载是通过不同的方法参数来区分的，如不同的参数个数，不同的参数类型，或不同的参数顺序
* 不能通过访问权限，抛出异常，返回值来进行重载

#### 覆盖

覆盖是指派生类方法覆盖基类方法。覆盖一个方法并对其重写，以达到不同的作用。
以下是有关覆盖的测试代码

```java

class Super {
    public int f() { return 2;}
    public Object g(Object string) {
        System.out.println ("Super g()!");
        return 3;
    }
}
public class SubClass extends Super {
    //!public float f() {return 2f;}   编译时会报错，因为父类有一个返回值为int的f()方法，而导出类是返回值为float的f()方法，即返回值不明确。
    @Override
    public Integer g(Object string) {   //Integer也是一个Object。
        System.out.println ("SubClass g()!");
        return 34;
    }
    public static void main(String[] args) {
        Super x = new SubClass ();
        Object y = x.g ("2");
        System.out.println ("the value of y :" + y);
    }
}

```

运行结果

```java

SubClass g()!
the value of y :34

```

* 覆盖要求参数列表相同，如g()方法中父类和子类的入参必须都得是Object,如果入参不一样，则不是覆盖，是派生类的新方法。
* 派生类中的覆盖方法必须要和基类中的被覆盖的方法有相同的函数名和参数。
* 派生类中的覆盖方法的返回值必须和基类中的返回值一样，但是基类返回值若是Object，则派生类返回值可以是其他类型（所有类都是继承自Object），如上面g()方法。
