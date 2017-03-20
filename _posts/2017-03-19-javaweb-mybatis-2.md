---
layout: post
title: mybatis学习(二)
keywords: Mybatis
categories: [JavaWeb]
tags: [JavaWeb]
---

####前言
本文主要讲述mybatis执行简单的查询语句的过程,有兴趣可以自己debug一下。(以mapper接口方式映射sql语句,Mybatis的最佳实践)

####正文

1. Reader reader = Resources.getResourceAsReader("conf.xml");  读取配置文件信息
2. 建立SqlSessionFactory,其中build方法主要解析配置文件,即XMLConfigBuilder解析mybatis的conf.xml
3. SqlSession sqlSession = sqlSessionFactory.openSession();   建议一个SqlSession(DefaultSqlSession),传入配置信息及executor,autoCommit
4. 通过MapperProxyFactory获取mapper,使用了java动态代理,注意此处是用对应mapping.xml的namespace + id去对应接口中的方法
5. 调用接口中的方法

##### mapper实现原理
MapperProxy类中invoke方法源码

```java
public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
    try {
      if (Object.class.equals(method.getDeclaringClass())) {
        return method.invoke(this, args);
      } else if (isDefaultMethod(method)) {
        return invokeDefaultMethod(proxy, method, args);
      }
    } catch (Throwable t) {
      throw ExceptionUtil.unwrapThrowable(t);
    }
    final MapperMethod mapperMethod = cachedMapperMethod(method);
    return mapperMethod.execute(sqlSession, args);
  }

```

此处对mapper接口中的方法做了本地缓存,然后执行MapperMethod中的execute方法。

最后用一张图总结下整个sql的执行过程:
![picture](/images/javaweb/sqlprocess.png)





