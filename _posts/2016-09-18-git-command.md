---
layout: post
title: git基本操作
keywords: Git
categories: [Git]
tags: [Git]
---
### 工作流
* 工作目录： 持有实际文件
* 暂存区（Index）： 类似于缓存区域，临时保存你的改动
* HEAD： 指向你最后一次提交的结果

### 添加和提交
 * 将修改的文件使用如下命令添加到暂存区： git add *（一般直接用该命令添加文件夹到暂存区）
 * 使用如下命令实际提交改动： git commit -m "代码提交信息"
 * 改动提交到了HEAD，但还没到远端仓库，使用 git push origin master 提交到远端仓库，可以把master换成任r何分支
 
 
 参见：
 [http://rogerdudler.github.io/git-guide/index.zh.html](http://rogerdudler.github.io/git-guide/index.zh.html)



