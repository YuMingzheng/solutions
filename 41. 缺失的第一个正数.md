---
title: 41. 缺失的第一个正数
date: 2025-01-11
tags:
  - 双指针
---

### 问题描述

[题目链接](https://leetcode.cn/problems/first-missing-positive/description/)

在一个未排序的数组中找到缺失的正整数。

只能用 $O(n)$ 的算法，不允许申请额外的空间。

### 解题思路

#### 方法一

`left` 指向当前待检查的元素，`left` 左边是已经检查过的元素；`right` 指向的和右边的元素是垃圾元素。每次从范围左边拿个数字出来，看看这个数字是不是在它该在的位置上。要是对了，就接着看下一个；要是不对，就根据情况把这个数字和别的位置的数字交换一下，或者把它扔到垃圾区去。通过不断缩小预期范围，逐步完成检查。

```java
class Solution {  
    public int firstMissingPositive(int[] nums) {  
        int left = 0;  
        int right = nums.length;  
        while (left < right) {  
            int currCheckNum = nums[left];  
            int expectedNum = left + 1;  
            int expectedNumRightBoundary = right;  
            int oriShouldPos = currCheckNum - 1;  
            if (currCheckNum == expectedNum) {  
                left++;  
            } else if (currCheckNum < expectedNum || currCheckNum > expectedNumRightBoundary  
                    || currCheckNum == nums[oriShouldPos]) {  
                swap(nums, left, right - 1);  
                right--;  
            } else {  
                swap(nums, left, oriShouldPos);  
            }  
        }  
        return left + 1;  
    }  
  
    private void swap(int[] nums, int a, int b) {  
        int temp = nums[a];  
        nums[a] = nums[b];  
        nums[b] = temp;  
    }  
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
