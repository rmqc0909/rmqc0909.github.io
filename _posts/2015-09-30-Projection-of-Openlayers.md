---
layout: post
title: OpenLayers之Projection概述
categories : [OpenLayers]
tags : [OpenLayers, Projection]
---
在最近的学习中，遇到了投影（Projection）在Web地图应用中的问题，刚好有时间来总结一下。

众所周知，地图是**不规则的椭球体**，如果我们将其展开到二维平面上，会发现地图与实际情况有出入。所以，人们提出
投影的方式来尽量减小失真的程度。至于等角投影、等面积投影之类的内容，学过地图投影知识的自然了解，此处不加赘述。

###OpenLayers中投影

在[OpenLayers官网](http://openlayers.org/)的[ol.proj](http://openlayers.org/en/v3.10.1/apidoc/ol.proj.html) API介绍中,
对Web地图的投影分类有相应的介绍，如下：

> When loaded, the library adds projection objects for EPSG:4326 (WGS84 geographic coordinates) and EPSG:3857 (Web or Spherical Mercator, as used for example by Bing Maps or OpenStreetMap), together with the relevant transform functions.

从中可以看出，在OSM、Bing Map等网络地图中，多采用墨卡托投影，EPSG：3857；而部分用户自己上传的数据为WGS 84坐标系，
EPSG：4326。通过OpenLayers的ol.proj对象可以对坐标进行转换，相应的api介绍查看官网相关内容。同时，如果想获取更多
坐标转换的内容，[Proj4js库](http://proj4js.org/)满足了这方面的需求。

![picture](/images/other/projofopenlayer.png)

###PostGIS中投影

当Web地图中不同数据层的投影不同时，除了前端调用第三方库进行转换，还可以在后端改变数据源的投影。

此处介绍PostGIS常用的投影变换方面的函数：

+ [ST_Transform](http://postgis.org/docs/ST_Transform.html)

语法为：

> geometry ST_Transform(geometry g1, integer srid);

将g1(geometry)转化为SRID对应的投影的坐标，同时返回转换成功的geometry。

        UPDATE table_name SET geom_column = ST_Transform(geom_column,4326)

+ [UpdateGeometrySRID](http://postgis.org/docs/UpdateGeometrySRID.html)

语法为：

        text UpdateGeometrySRID(varchar table_name, varchar column_name, integer srid);

官方的解释为：

        Updates the SRID of all features in a geometry column, geometry_columns metadata and srid. If it was enforced with constraints, the constraints will be updated with new srid constraint. If the old was enforced by type definition, the type definition will be changed.

例如：

        SELECT UpdateGeometrySRID('table','geom',3857);
