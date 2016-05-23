---
layout: post
title: HTTP请求头和返回头
categories : [HTTP]
tags : [HTTP]
---
每个HTTP的请求和响应都有相应的头部信息。其中请求头的信息为：

> **Accept**:浏览器能够处理的内容类型  
> **Accept-Charset**:浏览器能够显示的字符集  
> **Accept-Encoding**:浏览器能够处理的压缩编码  
> **Accept-Language**:浏览器当前设置的语言  
> **Cache-Control**:指定请求和响应遵循的缓存机制  
> **Connection**:浏览器与服务器之间连接的类型  
> **Cookie**:当前页面设置的任何 Cookie  
> **Host**:发出请求的页面所在的域  
> **Referer**:发出请求的页面的 URI。注意,HTTP 规范将这个头部字段拼写错了,而为保证与规范一致,也只能将错就错了。(这个英文单词的正确拼法应该是 referrer)  
> **User-Agent**:浏览器的用户代理字符串  

返回头的信息为：

> **Cache-Control**:max-age=3600 一个用于定义缓存指令的通用头标  
> **Content-Encoding**:web服务器支持的返回内容压缩编码类型  
> **Content-Type**:返回内容的MIME类型  
> **Date**:原始服务器消息发出的时间  
> **ETag**:请求变量的实体标签的当前值  
> **Server**:web服务器软件名称  
> **Set-Cookie**:设置Http Cookie  
> **Transfer-Encoding**:文件传输编码  
> **Vary**:告诉下游代理是使用缓存响应还是从原始服务器请求  

[**详细的解释**](http://tools.jb51.net/table/http_header)
