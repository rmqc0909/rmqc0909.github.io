---
layout: post
title: JavaScript之基本概念
categories : [JavaScript]
tags : [JavaScript]
---
利用闲暇时间，重新回顾下JavaScript基本语法，以期温故知新！

+ \<noscript>标签元素用于检测浏览器对JavaScript支持与否，只在下面两种情况下起作用：

> 浏览器不支持脚本;  
> 浏览器支持脚本,但脚本被禁用。

除此之外，浏览器不会呈现\<noscript>中的内容。

{% highlight html %}
<html>
    <head>
        <title>Example HTML Page</title>
            <script type="text/javascript" defer="defer" src="example1.js"></script>
            <script type="text/javascript" defer="defer" src="example2.js"></script>
    </head>
    <body>
        <noscript>
            <p>本页面需要浏览器支持(启用)JavaScript</p>
        </noscript>
    </body>
</html>
{% endhighlight %}

+ ECMAScript  引入了严格模式(strict mode)的概念,即在解本顶部或者函数体内添加：

    "use strict";
严格模式下,JavaScript 的执行结果会有很大不同。

+ ECMAScript 的变量是松散类型的,所谓松散类型就是可以用来保存任何类型的数据。换句话说,每个变量仅仅是一个用于保存值的占位符而已。

> 虽然省略 var 操作符可以定义全局变量,但不推荐这样的做法。因为在局部作用域中定义的全局变量很难维护,而且如果有意地忽略了 var 操作符,也会由于
> 相应变量不会马上就有定义而导致不必要的混乱。**给未经声明的变量赋值在严格模式下会导致抛出 ReferenceError 错误。**

+ JavaScript函数在传递参数时，接受到的形参是一个arguments的数组，arguments[0]为第一个参数，arguments[1]为第二个参数，以此类推；
因此在JavaScript中，函数的形参和实参没有个数上的对应的关系，如函数定义时定义了二个形参，而当函数调用时可以传入一个、两个甚至不传入参数
。同时，JavaScript没有函数重载的概念，当有多个同名函数定义时，取最后一次定义的函数，猜测其原因：JavaScript参数传递的非严格性、与JavaScript数据类型的
灵活性。

+ 无须指定函数的返回值,因为任何 ECMAScript 函数都可以在任何时候返回任何值。
