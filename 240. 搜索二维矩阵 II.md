---
title: 240. 搜索二维矩阵 II
date: 2025-01-13
tags:
  - 矩阵
---

### 问题描述

[题目链接](https://leetcode.cn/problems/search-a-2d-matrix-ii/description/)

在一个行和列的数字都从小到大排序的二维数组中，找到目标元素。

### 解题思路

#### 方法一

从右上角开始查找。如果当前元素大于目标值，向左移动，因为目标值可能出现在左边，下边可以不用看了，因为肯定大于目标。如果当前元素小于目标值，则向下移动，左侧区域可以忽略，因为数组是有序的，左边不可能包含目标值。

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int matrixWidth = matrix[0].length;
        int matrixHeight = matrix.length;
        int x = matrixWidth - 1;
        int y = 0;
        while (0 <= x && y < matrixHeight) {
            int currNum = matrix[y][x];
            if (currNum == target) {
                return true;
            } else if (currNum < target) {
                y++;
            } else {
                x--;
            }
        }
        return false;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(m + n)$

空间复杂度：$O(1)$
