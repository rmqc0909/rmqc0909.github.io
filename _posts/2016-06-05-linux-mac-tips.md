---
layout: post
title: mkdir
keywords: Linux
categories: [Linux]
tags: [Linux]
---
### mac终端命令之mkdir

* 建立多层目录：

{% highlight javascript %}
$ mkdir -p /User/Documents/my_soft/mvnrepo
{% endhighlight %}

### 一点点说明

* 建立多层目录，不能用mkdir命令直接创建多层目录,如：

{% highlight javascript %}
$ mkdir /User/Documents/my_soft/mvnrepo
{% endhighlight %}

### 补充
**-p**: 可以自行创建多层目录(不推荐)
**-m**: 配置文件的权限


