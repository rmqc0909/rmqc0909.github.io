---
layout: post
title: Node之RESTful应用
categories : [Node]
tags : [Node, RESTful]
---
###RESTful 应用的特点

REST不是一种具体的实现技术，而是一种软件架构风格。REST几乎是为HTTP协议量身定制的，在HTTP中协议中用URI来标识唯一的资源
，用GET、POST、PUT、DELETE等动词来操作资源，HTTP协议是无状态协议，可以通过Cache来提高性能。
基于REST的架构风格，可以用在Web服务中。 RESTful的网络服务较之基于SOAP和XML-RPC方式的网络服务更加简洁
高效。它直接使用HTTP协议就可以实现Web服务，不需要额外的封装协议和远程进程的调用。

HTTP 请求在 RESTful Web 服务中的典型应用：

![picture](/images/other/restful.png)

###使用 Node 创建 RESTful 应用

虽然用Node创建RESTful应用不需要什么框架，但是大部分还是会借助第三方比较成熟的框架，本文采用Express框架，它对原生的
http模块进行了一些封装，更易于使用。利用Express来暴露接口，如GET：获取、 POST：新增 、PUT：更新、DELETE：删除（这里的CRUD都是针对与一个资源而言的）
，然后利用前端技术来操作后台数据（Ajax等）。

推荐几个国外比较好的总结：

[http://cwbuecheler.com/web/tutorials/2014/restful-web-app-node-express-mongodb/](http://cwbuecheler.com/web/tutorials/2014/restful-web-app-node-express-mongodb/)

[https://scotch.io/tutorials/build-a-restful-api-using-node-and-express-4](https://scotch.io/tutorials/build-a-restful-api-using-node-and-express-4)

[http://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm](http://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm)

[http://pixelhandler.com/posts/develop-a-restful-api-using-nodejs-with-express-and-mongoose](http://pixelhandler.com/posts/develop-a-restful-api-using-nodejs-with-express-and-mongoose)

[http://coenraets.org/blog/2012/10/creating-a-rest-api-using-node-js-express-and-mongodb/](http://coenraets.org/blog/2012/10/creating-a-rest-api-using-node-js-express-and-mongodb/)

此外，Node也提供了相应的第三方模块[node-restful](http://benaugarten.com/node-restful/)
