---
layout: post
title: 构造器内部多态方法的行为
keywords: Java
categories: [Java]
tags: [Java]
---
### 先看下面一段代码
```java

package cn.tk.polymiorphism.constructor;

class Glyph {
    void draw() { System.out.println ("Glyph.draw()");}

    public Glyph() {
        System.out.println ("Glyph() before draw()");
        draw ();
        System.out.println ("Glyph() after draw()");
    }
}
class RoundGlyph extends Glyph {
    private int radius = 1;

    public RoundGlyph(int radius) {
        this.radius = radius;
        System.out.println ("RoundGlyph.RoundGlyph(), radius = " + radius);
    }

    @Override
    void draw() {
        System.out.println ("RoundGlyph.draw(), radius = " + radius);
    }
}

public class PolyConstructors {
    public static void main(String[] args) {
        new RoundGlyph (5);
    }
}

```

### 运行结果

```java

Glyph() before draw()
RoundGlyph.draw(), radius = 0
Glyph() after draw()
RoundGlyph.RoundGlyph(), radius = 5

```

### 初始化顺序

* 在其他任何事物发生之前，将分配给对象的存储空间初始化成二进制的零
* 调用基类构造器。此时，调用被覆盖后的draw()方法（要在调用RoundGlyph构造器之前调用），由于步骤1，此时radius的值0
* 按照声明的顺序调用成员的初始化方法
* 调用导出类的构造器主体

### 编写构造器准则

* 用尽可能简单的方法使对象进入正常的状态，如果可以的话，避免调用其他方法
* 在构造器内唯一能够安全调用的方法是基类中的final方法（也适用于private方法），这些方法不能被覆盖


