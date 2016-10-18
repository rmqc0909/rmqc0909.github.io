---
layout: post
title: 算法小程序-WiggleSort
keywords: Algorithm
categories : [Algorithm]
tags : [Algorithm]
---

### Problem Description
Given an unsorted array nums, reorder it such that nums[0]< nums[1]> nums[2]< nums[3].... 

#### Example:
* Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6].
* Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2]. 

### 主要思路：
* 找出中位数mid，并将中位数放到指定位置，即中位数之前的所有元素都小于中位数，中位数后面的元素都大于中位数
* 利用A[i]=nums[1+2*(i))%(nums.length &#124; 1]关系进行数组下标的映射，当i < nums.length/2（原数组的前一半元素），映射到奇数位，当i >= nums.length/2（原数组的后一半元素），映射到偶数位
* A[i]与mid进行比较，其实相当于把大于mid的元素放到奇数位置，小于mid的元素放到偶数位置

### Solution

```java
public class WiggleSort {
    public static void main(String[] args) {
        int[] nums = {1, 3, 2, 2, 3, 1};
        int size = nums.length;
        int mid;
        KthSmallest kthSmallest = new KthSmallest();
        if (size % 2 == 0) {
            kthSmallest.kthSmallest (nums, 0, size - 1, size / 2);
            mid = nums[size / 2 - 1];
        }
        else {
            kthSmallest.kthSmallest (nums, 0, size - 1, size / 2 + 1);
            mid = nums[size / 2];
        }
        int i = 0, j = 0, k = size - 1;
        System.out.println ("sorted: ");
        for (int x:
                nums) {
            System.out.print (x + "  ");
        }
        System.out.println ();
        System.out.println ("mid element: " + mid);
        //偶数位（对应原来数组的下标范围是[(length/2)--(length-1)]）：放小于中位数的元素    奇数位（对应原来数组的下标范围是[0--(length/2 - 1)]）：放大于中位数的元素
        //getAnInt (nums, i)奇数槽的下标，getAnInt (nums, j)当前下标，getAnInt (nums, k)偶数槽的下标
        while (j <= k) {
            if (nums[getAnInt (nums, j)] > mid) {
                kthSmallest.swap (nums, getAnInt (nums, j++), getAnInt (nums, i++));
            }
            else if (nums[getAnInt (nums, j)] < mid) {
                kthSmallest.swap (nums, getAnInt (nums, j), getAnInt (nums, k--));
            }
            else {
                ++j;
            }
        }
        System.out.println ("wiggleSort: ");
        for (int x:
                nums) {
            System.out.print (x + "  ");
        }
    }
    //数组下标映射，当i < nums.length/2，映射到奇数位，当i >= nums.length/2，映射到偶数位
    private static int getAnInt(int[] nums, int i) {
        return (1 + 2 * (i)) % (nums.length | 1);
    }
}
```

### Reault

```java
sorted: 
1  1  2  2  3  3  
mid element: 2
wiggleSort: 
2  3  1  3  1  2
```

### 一点点说明

该算法研究挺久的，其中利用**kthSmallest.kthSmallest**方法寻找中位数并将其放入指定位置参考之前写的文章

[http://rmqc0909.github.io/blog/2016/09/algorithm-k'th_smallest_element.html](http://rmqc0909.github.io/blog/2016/09/algorithm-k'th_smallest_element.html)

对于下标的映射也需要好好理解下，可以参考以下文章

[https://discuss.leetcode.com/topic/32920/o-n-time-o-1-space-solution-with-detail-explanations](https://discuss.leetcode.com/topic/32920/o-n-time-o-1-space-solution-with-detail-explanations)
