---
layout: post
title: mybatis学习(一)
keywords: Mybatis
categories: [JavaWeb]
tags: [JavaWeb]
---
#### 前言
虽然网上已经有很多关于Mybatis的文章,但我决定要写自己的一个系列,趁着辞职间隙可以好好梳理一下。
写mybatis系列文章的目的主要有以下原因:

* 自己能对这个框架有更深的理解
* 帮助新手快速应用一个框架

#### 学习方法
mybatis是个相对容易理解的优秀框架,我采用的是: 官方文档 + 优秀博客,后面我会贴出链接。

**NOTE**
不论是看官方文档还是博客,都要自己去实际操作一遍,别人写的博客也不一定完全正确,一定要自己实践。

#### 正文
整体思路: 先介绍Mybatis应用与实践,最后在介绍如何整合Spring + Mybatis。本文介绍如何搭建一个Mybatis工程。(以mapper接口方式映射sql语句,Mybatis的最佳实践)

开发工具: idea(一款很好的java开发工具哦~)

项目管理工具: maven(建议使用)

数据库: mysql

1. 建表

```java
create database mybatis;
CREATE TABLE `country` (
  `Id` int(11) NOT NULL AUTO_INCREMENT,
  `country_name` varchar(255) DEFAULT NULL,
  `country_code` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`Id`)
) ENGINE=InnoDB AUTO_INCREMENT=184 DEFAULT CHARSET=utf8;
```

2. 引入相关依赖,用maven搭建mybatis工程

```java
<jdbc.driver.version>5.1.27</jdbc.driver.version>
<mybatis.version>3.4.2</mybatis.version>
```

3. 配置conf.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC" />
            <!-- 配置数据库连接信息 -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis" />
                <property name="username" value="root" />
                <property name="password" value="root" />
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <!-- Using classpath relative resources -->
        <mapper resource="com/github/mapping/Country.xml"></mapper>
    </mappers>
</configuration>

```

4. 测试demo

```java
public class MapperInterfaceTest {

    private Reader reader;

    private SqlSessionFactory sqlSessionFactory;

    @Before
    public void setUp() throws Exception {
        try {
            reader = Resources.getResourceAsReader("conf.xml");
        } catch (IOException e) {
            e.printStackTrace();
        }
        sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
    }


    @Test
    public void testGetCountryById() {
        SqlSession sqlSession = sqlSessionFactory.openSession();
        try {
            CountryMapper countryMapper = sqlSession.getMapper(CountryMapper.class);
            Country country = countryMapper.getCountryById(184);
            System.out.println(country);
        } finally {
            sqlSession.close();
        }
    }
 }

```

bean,mapper,以及xml可看github源码。

综上,一个简单的mybatis入门工程搭建完毕。


#### 后记
[mybatis官方文档](http://www.mybatis.org/mybatis-3/zh/getting-started.html)

[mybatis学习博客](https://my.oschina.net/zudajun/blog)

[本文demo源码](https://github.com/rmqc0909/keep.git)

