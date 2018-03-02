---
layout: post
title: 梯度下降法
keywords: MachineLearning
categories: [ML]
tags: [ML]
---
### 梯度
梯度是一个矢量，其方向上的方向导数最大，其大小正好是此最大方向导数。
1. 梯度方向：方向导数最大的方向
2. 梯度值：方向导数最大值

### 梯度下降法求解线性回归问题
针对下式

![picture](/images/machinelearing/grad1.png)

其中x0 = 1，m为样本数，n为特征数，theta为线性回归的参数；
1. 代价函数

![picture](/images/machinelearing/grad2.png)

2. 求梯度

![picture](/images/machinelearing/grad3.png)

3. 参数更新

![picture](/images/machinelearing/grad4.png)

* 梯度下降法在遇到局部最优解时，将停止更新参数；
* **Batch Gradient Descent**:  Each step of gradient descent uses all the training examples.
* 梯度下降法在学习率（learning rate）固定（步长不能太大）的情况下，随着迭代次数的增加，更新速度会变缓，即越接近局部（全局）最小时，收敛速度越慢。
* 两个参数的代价函数是一个3D的碗状图形，三个坐标轴分别代表了两个参数theta_0,theta_1和代价函数J(theta_0,theta_1)。如下

![picture](/images/machinelearing/grad5.png)

通常，用轮廓图来表示这种3D图片，如下

![picture](/images/machinelearing/grad6.png)

上右即为轮廓图。在同一个椭圆上的各个点，J(theta_0,theta_1)的值是相同的，而越靠中心的椭圆则J（代价函数）值越小。

### 批梯度下降（BGD） 随机梯度下降（SGD）

* 批梯度下降

更新参数时使用所有的样本
* 随机梯度下降

更新参数时使用一个样本

示例代码详见 https://github.com/rmqc0909/ML-linear_regression.git


