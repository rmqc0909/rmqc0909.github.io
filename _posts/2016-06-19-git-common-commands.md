---
layout: post
title: git命令学习
keywords: git
categories : [Git]
tags : [Git]
---
### 如何在idea中更新git上的代码

命令行中利用git命令

更新代码

* git pull

如果出现代码冲突:
{% highlight javascript %}
error: Your local changes to the following files would be overwritten by merge
        .......
Please, commit your changes or stash them before you can merge.
{% endhighlight %}
可将代码库的文件完全覆盖本地工作版本,方法如下

覆盖本地工作版本

* git reset --hard(两个-)
* git pull
