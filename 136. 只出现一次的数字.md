---
title: 136. 只出现一次的数字
date: 2025-01-07
tags:
  - 位运算
---

### 问题描述

[题目链接](https://leetcode.cn/problems/single-number/description/)

在一个数组中，其他数字都成对出现，只有一个数字只出现一次，找出那个孤儿数字。

### 解题思路

#### 方法一

异或运算的性质是：相同的数互相抵消为 0。由于数组中的数字总是成对出现，遍历数组中的每个数，把它们异或到一起，经过异或运算后，最终只会剩下一个孤独的数字，因为没有其它的数可以跟它消。

```java
class Solution {
    public int singleNumber(int[] nums) {
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }
        return xor;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
