---
layout: post
title: Centos下Tilemill安装问题
categories : [Tilemill]
tags : [Tilemill, Nodejs, Centos]
---
对Ubuntu的社区支持远胜于Centos，可能与各自的功能与特性有关。Ubuntu下软件的安装和环境配置非常简单，如本题Tilemill安装为例，前往
[https://www.mapbox.com/tilemill/](https://www.mapbox.com/tilemill/)下载解压后，double-click即可。

由于Centos的稳定性较强，多用于企业级服务器，在普通Linux爱好者中使用范围不及Ubuntu。对于本文Tilemill在Centos下的安装，需要前往[https://github.com/mapbox/tilemill](https://github.com/mapbox/tilemill)
下载源码进行编译。

+ 安装依赖（Depends）

> Mapnik v2.3.0  
> Node.js v0.10.x or v0.8.x  
> Protobuf: libprotobuf-lite and protoc

+ 下载源码

        git clone https://github.com/mapbox/tilemill.git

+ 编译

        cd tilemill
        npm install

+ 启动

        ./index.js

服务启动后，在浏览器输入**localhost:20009**，即可。

从安装依赖（Depends）中可以看出，Tilemill的支持的Nodejs版本为v0.10.x or v0.8.x，如果电脑安装的Nodejs版本为v0.12 or up，会出现下面的问题：

> tilemill/node_modules/tilelive/lib/statistics.js:24  set remaining() {}, // read-only
