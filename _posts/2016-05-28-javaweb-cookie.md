---
layout: post
title: cookie学习
keywords: cookie
categories: [JavaWeb]
tags: [JavaWeb]
---
### 为什么要有cookie
先解释两个名词：客户端和服务器端。

#### 客户端：可以理解为你的浏览器

#### 服务端：姑且认为是高级PC吧。

当客户端在发送一个请求并且得到返回信息之后，客户端和服务器端之间的网络连接就已经断开，在发送下一个请求时，服务器端无法确定这次请求和上次的请求是否来自同一个客户端。即，服务器不能“记住”用户，这是因为http协议是无状态的协议。而在web应用程序中，是经常需要记住每次请求的。
为了让服务器知道不同的请求是否来自同一个客户端。于是出现了cookie和session。

### cookie是什么 

cookie是一个数据包，每次访问网站的时候浏览器都会将该网站的cookie发回给网站服务器，cookie不是只有一个，而是一个网站一个，它是你在某个网站上的唯一标识。cookie由服务器端生成。

### 使用cookie 的关键代码:


建立一个无生命周期的cookie
{% highlight javascript %}
    HttpServletRequest request  
    HttpServletResponse response
    Cookie cookie = new Cookie("cookiename","cookievalue");
    response.addCookie(cookie);
{% endhighlight %}

读取cookie
{% highlight javascript %}
    Cookie[] cookies = request.getCookies();
    for(Cookie cookie : cookies){
    cookie.getName() 
    cookie.getValue(); 
}
{% endhighlight %}



