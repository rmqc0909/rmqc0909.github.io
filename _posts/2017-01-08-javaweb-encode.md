---
layout: post
title: Webserver下控制台中文显示为 ？
keywords: encode
categories : [JavaWeb]
tags : [JavaWeb]
---
### 开发环境
首先声明,出现中文不显示问题仅限于webserver下,执行java的main函数是显示中文的

* 操作系统: Mac   
* 开发工具:Idea

### 解决方法

1. 打开idea安装目录下（软件一般都安装在/Applications目录）/Applications/IntelliJ IDEA 15.app/Contents/bin   
idea.vmoptions文件    -—-该文件是jvm运行时的参数配置
2. 在idea.vmoptions文件末尾添加：-Dfile.encoding=UTF-8
3. 打开idea中配置的tomcat界面，在VM option处也添加  -Dfile.encoding=UTF-8

参见 [http://www.kafeitu.me/tools/2013/03/26/intellij-deal-chinese-disorderly-code.html](http://www.kafeitu.me/tools/2013/03/26/intellij-deal-chinese-disorderly-code.html)







