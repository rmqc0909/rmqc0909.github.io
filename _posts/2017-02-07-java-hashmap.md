---
layout: post
title: HashMap之put(K key, V value)方法学习
keywords: Java
categories: [Java]
tags: [Java]
---
JDK版本：1.7

HashMap采用的数据结构：哈希数组
处理冲突的方法：链地址法（拉链法）

```java
public V put(K key, V value) {
        if (table == EMPTY_TABLE) {
            inflateTable(threshold);    //1
        }
        if (key == null)
            return putForNullKey(value);    //2
        int hash = hash(key);   //3
        int i = indexFor(hash, table.length);   //4
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }   //5

        modCount++;     //6
        addEntry(hash, key, value, i);  //7
        return null;
    }
```


1. 该处主要用来初始化一个长度为2的幂次方的数组（table[]，数组中的每个元素可以看作是一个桶**bucket**）,其中主要的方法有roundUpToPowerOf2(toSize)，记住这个方法的返回值是第一个大于toSize并且是2的幂次的整数就行。
2. 当key为null时，先在table[0]的链表中寻找null key，如果有null key就直接覆盖原来的value，返回原来的value；如果在table[0]中没有找到，就进行头插，但是要先判断是否要扩容，需要就扩容，然后进行头插；
3. 该方法主要作用是防止质量较差的哈希函数带来过多的冲突（碰撞）问题，相当于对key进行了二次散列。
4. 该方法相当于**hash % table.length**。
5. 该处的for循环用于检查这个key值是否已经存在于这个map中（同时比较hash值和key值），若存在，则用新value替换旧的value，并返回旧value。
6. 该变量用于计算这个map被修改的次数。
7. 若这个key在map中不存在，则将该key添加进来。

再详细看下addEntry()方法

```java

void addEntry(int hash, K key, V value, int bucketIndex) {
        if ((size >= threshold) && (null != table[bucketIndex])) {
            resize(2 * table.length);   //8
            hash = (null != key) ? hash(key) : 0;
            bucketIndex = indexFor(hash, table.length); //9
        }

        createEntry(hash, key, value, bucketIndex);     //10
    }
```

8. 当map.size大于threshold时，需对table[]进行扩容。
再看下resize方法

```java

void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }

        Entry[] newTable = new Entry[newCapacity];
        transfer(newTable, initHashSeedAsNeeded(newCapacity));
        table = newTable;
        threshold = (int)Math.min(newCapacity * loadFactor, MAXIMUM_CAPACITY + 1);
    }
    
    void transfer(Entry[] newTable, boolean rehash) {
        int newCapacity = newTable.length;
        for (Entry<K,V> e : table) {
            while(null != e) {
                Entry<K,V> next = e.next;
                if (rehash) {
                    e.hash = null == e.key ? 0 : hash(e.key);
                }
                int i = indexFor(e.hash, newCapacity);
                e.next = newTable[i];
                newTable[i] = e;
                e = next;
            }
        }
    }    
```

该方法两个作用，一是扩容，二是将原来table[]中的所有entries移到新扩容的new_table[]中，并且在transfer原表内容的时候链表被倒置了。

9. 计算扩容后的hash(key)对应的桶的位置。
10. 添加新的Entry。

以下是createEntry()方法

```java

void createEntry(int hash, K key, V value, int bucketIndex) {
        Entry<K,V> e = table[bucketIndex];
        table[bucketIndex] = new Entry<>(hash, key, value, e);
        size++;
    }
    
```

从以上代码可以看出，每创建一个新的Entry，都会放到table[bucketIndex]的位置，然后将原来的Entry放在新创建Entry的后面，并且map.size加1。


#### HashMap无序性原因

从上面代码中，可以看出HashMap之所以不能保持元素的顺序有以下几点原因:

1. 插入元素的时候对元素进行哈希处理，不同元素分配到table的不同位置（即桶的位置）。
2. 容量拓展的完又对key重新进行了hash处理。
3. 在transfer原表内容的时候链表被倒置了。


