---
layout: post
title: JavaScript之面向对象
categories : [JavaScript]
tags : [JavaScript]
---
ECMAScript中有两种属性:数据属性和访问器属性，放在两个方括号中：

+ 数据属性，包含一个数据值的位置，这个位置可以读取或者写入数值。
  - [[Configurable]]：表示能否通过delete删除属性从而重新定义属性，能否修改属性的特征，能否把属性修改为访问器属性。
  默认值为true。
  - [[Enumerable]]:表示能否通过 for-in 循环返回属性，默认值为 true。
  - [[Writable]]:表示能否修改属性的值，默认值为 true。
  - [[Value]]:包含这个属性的数据值。读取属性值的时候,从这个位置读;写入属性值的时候,把新值保存在这个位置。默认值为 undefined。

  要修改属性默认的特性,必须使用 ECMAScript 5 的 Object.defineProperty()方法。这个方法三个参数:属性所在的对象、属性的名字和一个描述符对象。其中,描述符(descriptor)对象的属
性必须是:configurable、enumerable、writable 和 value。设置其中的一或多个值,可以修改对应的特性值。
{% highlight javascript %}
var person = {};
Object.defineProperty(person, "name", {
    writable: false,
    value: "Nicholas"
});
alert(person.name); //"Nicholas"
person.name = "Greg";
alert(person.name); //"Nicholas"
{% endhighlight %}

+ 访问器属性，访问器属性不包含数据值。在读取访问器属性时,会调用 getter 函数,这个函数负责返回有效的值;在写入访问器属性时,会调用
setter 函数并传入新值,这个函数负责决定如何处理数据。
  - [[Configurable]]:表示能否通过 delete 删除属性从而重新定义属性,能否修改属性的特性,或者能否把属性修改为数据属性。默认值为
true。
  - [[Enumerable]]:表示能否通过 for-in 循环返回属性。默认值为 true。
  - [[Get]]:在读取属性时调用的函数。默认值为 undefined。
  - [[Set]]:在写入属性时调用的函数。默认值为 undefined。

+ 构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。这样，每个实例都会有自己的一份实例属性的副本,
但同时又共享着对方法的引用,最大限度地节省了内存。
{% highlight javascript %}
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ["Shelby", "Court"];
}
Person.prototype = {
    constructor : Person,
    sayName : function(){
        alert(this.name);
    }
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
person1.friends.push("Van");
alert(person1.friends);//"Shelby,Count,Van"
alert(person2.friends);//"Shelby,Count"
alert(person1.friends === person2.friends);//false
alert(person1.sayName === person2.sayName);//true
{% endhighlight %}

+ 如果在已经创建了实例的情况下修改原型，会切断现有实例与新原型之间的联系。

+ 构造函数、原型和实例的关系:每个构造函数都有一个原型对象,原型对象都包含一个指向构造函数的指针,而实例都包含一个指向原型
对象的内部指针。

+ JavaScript 主要通过原型链实现继承。原型链的构建是通过将一个类型的实例赋值给另一个构造函数的原型实现的。这样,子类型就能够访问超类型的所有属性和方法,这一点与基于类的继承很相似。
