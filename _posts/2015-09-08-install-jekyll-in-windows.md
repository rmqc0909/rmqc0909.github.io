---
layout: post
title: 如何在Windows下安装Jekyll
keywords: Windows, Jekyll
categories : [Software]
tags : [Jekyll, Windows]
---
目前，网上关于在Windows下安装Jekyll的教程很多，今天总结一下，大致的流程如下：

- 安装Ruby
- 安装DevKit
- 安装Jekyll
- 安装Pygments
  + 安装Python
  + 安装Easy Install
  + 安装Pygments

##安装Ruby
+ 前往[RubyInstall for Windows](http://rubyinstaller.org/downloads/)下载Ruby最新安装包
+ 双击安装在选择不带空格的文件夹内，选 “Add Ruby executables to your PATH”，Ruby路径添加到系统变量中
+ 打开cmd命令框来检查Ruby是否安装成过

        ruby -v

##安装DevKit
DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。

+ 前往Ruby软件包下载中心[下载](http://rubyinstaller.org/downloads/)，注意选择与Ruby版本对应的DevKit包
+ 运行安装并解压至C:\DevKit，同时通过初始化来创建config.yml 文件。在命令行中依此输入：

        cd “C:\DevKit”  
        ruby dk.rb init  
        notepad config.yml

+ 在打开的记事本窗口中，于末尾添加新的一行 - C:\Ruby（Ruby安装的路径），保存文件并退出

##安装 Jekyll
+ 确保gem已经安装成功

        gem -v

+ 安装 Jekyll

        gem install jekyll

##安装Pygments
pygments是jekyll中默认的高亮插件，在_config.yml中添加highlights: pygments

- 安装Python，确保安装路径在系统环境变量中(容易解决)
- 安装Easy Install
  + 下载保存[ez_setup.py](https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py),并用python编译
  + 添加 ‘Python Scripts’ 路径 (如： C:\Python27\Scripts) 至 PATH
- 安装 Pygments

在确保Easy Install安装完成的基础上，安装pygments：

    easy_install pygments

##启动 Jekyll
    jekyll new blog
    cd blog
    jekyll build --trace
    jekyll server

<strong style = "color:red">如果cmd显示permission denied,可能的原因为端口被占用了，修改_config.yml中port的值</strong>
