---
layout: post
title: strategy学习
keywords: strategy
categories : [Design]
tags : [Design]
---
### 概述

策略模式属于对象的行为模式。其用意是针对一组算法，将每一个算法封装到具有共同接口的独立的类中，从而使得它们可以相互替换。策略模式使得算法可以在不影响到客户端的情况下发生变化。

### 策略模式概述  

策略模式属于对象的行为模式。  
其用意是针对一组算法，将每一个算法封装到具有共同接口的独立的类中，从而使得它们可以相互替换。   策略模式使得算法可以在不影响到客户端的情况下发生变化。

#### 该模式涉及到三个角色：  

环境(Context)角色  
抽象策略(Strategy)角色  
具体策略(ConcreteStrategy)角色

### 源代码

环境角色类

{% highlight javascript %}
    package cn.tk.study.strategy2;

	public class Context 
	{
		
		private Strategy strategy;
		
		public Context(Strategy strategy) 

			this.strategy = strategy;
		}
		
		public void setStrategy(Strategy strategy) 
		{
			this.strategy = strategy;
		}
		public void operate()
		{
			strategy.operate();
		}
	}

{% endhighlight %}

抽象策略类

{% highlight javascript %}
	package cn.tk.study.strategy2;
	
	public interface Strategy 
	{
		
		public void operate();
	
	}
{% endhighlight %}

具体策略类

{% highlight javascript %}
    package cn.tk.study.strategy2;

	public class BackDoor implements Strategy 
	{
		@Override
		public void operate() 
		{
			System.out.println("计策1！！！");
		}
	
	}
{% endhighlight %}

{% highlight javascript %}
    package cn.tk.study.strategy2;

	public class BlackEnemy implements Strategy 
	{
		@Override
		public void operate() 
		{
			System.out.println("计策3！！！");
		}
	}
{% endhighlight %}

{% highlight javascript %}
    package cn.tk.study.strategy2;

	public class GivenGreenLight implements Strategy 
	{
		@Override
		public void operate() 
		{
			System.out.println("计策2！！！");
		}
	
	}
{% endhighlight %}

测试类

{% highlight javascript %}
    package cn.tk.study.strategy2;

	public class Invoke {
	
		public static void main(String[] args) {
			Context context;
			context = new Context(new BackDoor());
			context.operate();
			System.out.println("\n");  
			context.setStrategy(new GivenGreenLight());
			context.operate();
			System.out.println("\n");  
			context.setStrategy(new BlackEnemy());
			context.operate();
			System.out.println("\n");  
		}
	
	}
{% endhighlight %}

运行结果

![picture](/images/designpattern/strategyrunreaults.png)
