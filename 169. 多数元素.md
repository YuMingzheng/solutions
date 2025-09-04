---
title: 169. 多数元素
date: 2025-01-07
tags:
  - 摩尔投票
---

### 问题描述

[题目链接](https://leetcode.cn/problems/majority-element/description/)

在一个数组中，找到出现次数超过数组长度一半的数。

### 解题思路

#### 方法一

摩尔计数。

如果一个元素的出现次数超过数组长度的一半，那么即使将所有与它不同的元素都抵消掉，最后剩下的元素仍然是这个众数。正因为众数拥有足够多的支持者，即使在过程中遭遇了一些“反对”，它依然能够在最后的“选举”中胜出。

**第一步：找出候选人。**

1. 初始化候选元素 `candidate` 为数组的第一个元素，计数器 `count` 为 1。
2. 遍历数组的每个元素：
	- 如果当前元素和 `candidate` 相同，计数器 `count++`。
	- 如果当前元素和 `candidate` 不同，计数器 `count--`。
	- 如果 `count` 减到 0，则将当前元素设为新的 `candidate`，并将 `count` 重置为 1。

**第二步：验证候选人。**

1. 遍历数组，统计 `candidate` 的实际出现次数。
2. 如果出现次数大于数组长度的一半，则 `candidate` 是众数；否则数组中不存在这样的元素。

只有在数组中确实存在出现次数超过一半的元素时，这个算法才管用。

```java
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = 0;
        int count = 0;
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
                count++;
            } else if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }
        return candidate;
    }
}
```

题目确保必有众数，所以不用验证了。

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
