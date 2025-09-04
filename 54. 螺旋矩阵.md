---
title: 54. 螺旋矩阵
date: 2025-01-12
tags:
  - 矩阵
---

### 问题描述

[题目链接](https://leetcode.cn/problems/spiral-matrix/description/)

顺时针遍历二维数组，上、右、下、左，一直循环，直到全部元素都被遍历完。

### 解题思路

#### 方法一

维护 4 个边界：上、右、下、左。遍历完 1 层移动边界，如果边界错位则跳出循环。

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> ans = new ArrayList<>();
        int left = 0;
        int right = matrix[0].length - 1;
        int top = 0;
        int bottom = matrix.length - 1;
        while (true) {
            for (int i = left; i <= right; i++) {
                ans.add(matrix[top][i]);
            }
            if (++top > bottom) {
                break;
            }
            for (int i = top; i <= bottom; i++) {
                ans.add(matrix[i][right]);
            }
            if (--right < left) {
                break;
            }
            for (int i = right; i >= left; i--) {
                ans.add(matrix[bottom][i]);
            }
            if (--bottom < top) {
                break;
            }
            for (int i = bottom; i >= top; i--) {
                ans.add(matrix[i][left]);
            }
            if (++left > right) {
                break;
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n \times m)$

空间复杂度：$O(1)$
