---
title: 9. 回文数
date: 2025-01-06
tags:
  - 双指针
---

### 问题描述

[题目链接](https://leetcode.cn/problems/palindrome-number/description/)

判断一个数字是否从左往右读和从右往左读都相同。

### 解题思路

#### 方法一

首先将数字转换为字符串，然后使用双指针算法：一个指针从左向右移动，另一个从右向左移动。每一步比较两个指针所指向的字符是否相同。

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        String x_str = String.valueOf(x);
        int i = 0;
        int j = x_str.length() - 1;
        while (i < j) {
            char i_char = x_str.charAt(i);
            char j_char = x_str.charAt(j);
            if (i_char != j_char) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$

#### 方法二

使用 $\log_{10}(x)$ 可以快速确定数字 `x` 是几位数。然后通过数学运算提取其最高位和最低位进行比较，比较后将数字除以 10，重复此过程，直到数字变为 0。

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        int digitCount = (int) Math.log10(x) + 1;
        int divisor = (int) Math.pow(10, digitCount - 1);
        while (x != 0) {
            if (x % 10 != x / divisor) {
                return false;
            }
            x = (x % divisor) / 10;
            divisor /= 100;
        }
        return true;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
