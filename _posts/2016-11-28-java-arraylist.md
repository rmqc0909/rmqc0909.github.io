---
layout: post
title: ArrayList学习
keywords: Java
categories : [Java]
tags : [Java]
---
#### add方法分析

ArrayList类中add方法返回一个boolean值，并且ArrayList是数组实现，方法体主要包含了两个方法：

* ensureCapacityInternal(size + 1);
* elementData[size++] = e;  将元素e放入集合elementData中

#### 测试代码

```java
@Test
	public void test() {
        ArrayList<Integer> arrayList = new ArrayList(); //1
        ArrayList<Integer> caparrayList = new ArrayList(1000);  //2
        for (int i = 0; i < 100; i++) arrayList.add(i);
	}
```

* 方式1 new ArrayList()对应的size初值为0，本篇主要讲述第一种情况ArrayList中自动扩容及如何增加元素。
* 方式2 new ArrayList(1000)直接初始化一个大小是1000的数组。

#### add方法源码

```java

    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    
    transient Object[] elementData; 
    
    private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;


    /**
     * Default initial capacity.
     */
    private static final int DEFAULT_CAPACITY = 10;

    private void ensureCapacityInternal(int minCapacity) {
            if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
                minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);      //第一次给容器分配的size为10
            }
    
            ensureExplicitCapacity(minCapacity);
    }
    
    private void ensureExplicitCapacity(int minCapacity) {
        modCount++;     //记录这个list结构（size属性）被修改过的次数

        // overflow-conscious code
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }
    //自动扩容，新容器大小是旧容器的1.5倍
    private void grow(int minCapacity) {
            // overflow-conscious code
            int oldCapacity = elementData.length;
            int newCapacity = oldCapacity + (oldCapacity >> 1);
            if (newCapacity - minCapacity < 0)
                newCapacity = minCapacity;
            if (newCapacity - MAX_ARRAY_SIZE > 0)
                newCapacity = hugeCapacity(minCapacity);
            // minCapacity is usually close to size, so this is a win:
            elementData = Arrays.copyOf(elementData, newCapacity);
    }
    
```
    
#### 源码补充说明

* modCount:这个字段是由迭代器和列表迭代器实现的，如果此字段的值意外更改，则迭代器(list迭代器) 将在响应迭代器的next方法，remove方法，previous(),set(),add()等方法抛出concurrentmodificationexception异常，这提供了快速失败的行为，而不是在面对迭代过程中，并发修改的非确定性行为。



   



    