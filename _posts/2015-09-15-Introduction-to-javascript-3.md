---
layout: post
title: JavaScript之引用类型
categories : [JavaScript]
tags : [JavaScript]
---
+ JavaScript中Array类型数据，自带的sort()排序方法工作原理：先调用每个数组项的 toString()转型方法,然后比较得到的字符串，
然后比较字符串，此时就会出现数字5在数字10之后的情况。解决方法：定义一个compare()函数，然后array1.sort(compare)进行排序。

+ arguments 的主要用途是保存函数参数,但这个对象有一个名叫 callee 的属性,该属性是一个指针,指向拥有这个 arguments 对象的函数。   
经典的阶乘函数：
{% highlight javascript %}
function factorial(num){
    if (num <=1) {
        return 1;
    } else {
    return num * arguments.callee(num-1);
    }
}
{% endhighlight %}

+ Math.ceil()、Math.round ()、Math.floor()分别为进一法、四舍五入和保留整数法。

+ 每个基本类型都有与之对应的基本包装类型：Boolean、Number 和 String。在访问基本类型值时,就会创建对应的基本包装类型的一个对象,从而方便了数据
操作;操作基本类型值的语句一经执行完毕,就会立即销毁新创建的包装对象。
