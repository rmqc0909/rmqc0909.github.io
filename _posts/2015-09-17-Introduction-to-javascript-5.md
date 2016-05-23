---
layout: post
title: JavaScript之函数表达式
categories : [JavaScript]
tags : [JavaScript]
---
+ 作用域链本质上是一个指向变量对象的指针列表,它只引用但不实际包含变量对象。在函数中访问一个变量时,就会从作用域链中搜索具有相应名字的变量。一般来讲,
当函数执行完毕后,局部活动对象就会被销毁,内存中仅保存全局作用域(全局执行环境的变量对象)。

+ 在使用闭包时，如果想访问作用域中的**arguments**和**this**对象，必须将对该对象的引用保存到另一个闭包能够访问的变量中。

+ 闭包会引用包含函数的整个活动对象。

+ 函数声明后面不能添加圆括号，而函数表达式后面可以跟圆括号。如果要将函数声明转换成函数表达式，用括号将函数声明包裹起来即可。

+ 可以在 JavaScript 中模仿块级作用域(JavaScript 本身没有块级作用域的概念)，创建并立即调用一个函数,这样既可以执行其中的代码,又不会在内存中留下对该函数的引用。

+ 即使 JavaScript 中没有正式的私有对象属性的概念,但可以使用闭包来实现公有方法,而通过公有方法可以访问在包含作用域中定义的变量。

在Javascript中实现单例模式如下：
{% highlight javascript %}
var singleton = function () {
    //私有变量和私有函数
    var privateVariable = 10;

    function privateFunction() {
        return false;
    };

    //特权/公有方法和属性
    return {
        publicProperty: true,

        publicdMethod: function() {
            privateVariable ++;
            return privateVariable();
        };
    };
}();
{% endhighlight %}
