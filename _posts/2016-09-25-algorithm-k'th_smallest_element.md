---
layout: post
title: 算法小程序-Find_K'th_Smallest_Element(Expected Linear Time)
keywords: Algorithm
categories: [Algorithm]
tags: [Algorithm]
---

### Problem Description
Given an array and a number k where k is smaller than size of array, we need to find the k’th smallest element in the given array. 

### 该算法主要思路:

* 先随机产生一个整数pivot(介于数组下标之间)
* 将pivot与数组最右边元素作交换
* 以数组最右边元素为游标,进行快排,一次快排结果即会将该数组最右边元素放入指定位置
* 比较pivot与k的的相对位置
* k < piovt,递归左半部分, k > pivot,递归右半部分, 依次重复前面步骤, k = pivot,则array[pivot]即为数组第k小元素
* 每次将随机产生的pivot与数组最右边元素作交换,只是为了将pivot的位置变得特殊,以简化快排的复杂度


### Solution

```java

package cn.tk.leetcode;


import java.util.Random;

/**
 * Created by xiedan on 16/9/21.
 */
public class KthSmallest {
    /* This function returns k'th smallest element in arr[l..r]
     using QuickSort based method.  ASSUMPTION: ALL ELEMENTS
     IN ARR[] ARE DISTINCT*/
    int kthSmallest(int arr[], int l, int r, int k)
    {
        // If k is smaller than number of elements in array
        if (k > 0 && k <= r - l + 1)
        {
            // Partition the array around a random element and
            // get position of pivot element in sorted array
            int pos = randomPartition(arr, l, r);

            // If position is same as k
            if (pos-l == k-1)
                return arr[pos];

            // If position is more, recur for left subarray
            if (pos-l > k-1)
                return kthSmallest(arr, l, pos-1, k);

            // Else recur for right subarray
            return kthSmallest(arr, pos+1, r, k-pos+l-1);
        }

        // If k is more than number of elements in array
        return Integer.MAX_VALUE;
    }

    // Utility method to swap arr[i] and arr[j]
    void swap(int arr[], int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    /* Standard partition process of QuickSort().  It considers
     the last element as pivot and moves all smaller element
     to left of it and greater elements to right. This function
     is used by randomPartition()*/
    int partition(int arr[], int l, int r)
    {
        int x = arr[r], i = l;
        //保证i之前的元素均小于数组最右边的元素
        for (int j = l; j < r; j++)
        {
            if (arr[j] <= x)
            {
                swap(arr, i, j);
                i++;
            }
        }
        swap(arr, i, r);
        return i;
    }

    /* Picks a random pivot element between l and r and
     partitions arr[l..r] arount the randomly picked
     element using partition()*/
    int randomPartition(int arr[], int l, int r)
    {
        Random rand = new Random();
        int n = r-l+1;
        int pivot = rand.nextInt(n);        //return a Integer between [0, n);
        swap(arr, l + pivot, r);
        return partition(arr, l, r);
    }

    // Driver method to test above
    public static void main(String args[])
    {
        KthSmallest ob = new KthSmallest();
        int arr[] = {12, 3, 5, 7, 4, 19, 26, 29, 3, 5, 36, 42};
        int n = arr.length,k = n / 2;
        System.out.println("K'th smallest element is "+
                ob.kthSmallest(arr, 0, n-1, k));
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}

```

### Result

```java

K'th smallest element is 7
3 4 3 5 5 7 12 29 19 26 36 42  

```

### 一点点说明

该算法是源代码出自,做了小部分修改:

[http://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/](http://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)



