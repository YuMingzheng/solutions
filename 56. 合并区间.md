---
title: 56. 合并区间
date: 2025-01-09
tags:
  - 模拟
---

### 问题描述

[题目链接](https://leetcode.cn/problems/merge-intervals/description/)

将重叠的区间合并后，返回一个不重叠的区间数组。

### 解题思路

#### 方法一

先根据二维数组中每个一维数组的第一个元素对其进行从小到大的排序。

遍历数组中的每个元素，按照以下逻辑判断：
- 如果前一个元素的尾端大于当前元素的头段：
    - 如果前一个元素的尾端也大于当前元素的尾端，说明当前元素被前一个元素包含。
    - 如果前一个元素的尾端小于当前元素的尾端，则将前一个元素的尾端扩展到当前元素的尾端位置。
- 如果前一个元素的尾端等于当前元素的头段：
	- 则将前一个元素的尾端扩展到当前元素的尾端位置。
- 如果前一个元素的尾端小于当前元素的头段：
    - 将手上持有的元素添加到结果中。
    - 然后将当前元素拿到手上。

手上拿着一个正在处理的元素，只有把它处理完了才放到结果中。

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> ans = new ArrayList<>();
        int[] prevInterval = new int[2];
        for (int i = 0; i < intervals.length; i++) {
            if (i == 0) {
                prevInterval = intervals[0];
            } else {
                int[] currInterval = intervals[i];
                if (prevInterval[1] > currInterval[0]) {
                    if (prevInterval[1] >= currInterval[1]) {
                        continue;
                    } else {
                        prevInterval[1] = currInterval[1];
                    }
                } else if (prevInterval[1] == currInterval[0]) {
                    prevInterval[1] = currInterval[1];
                } else {
                    ans.add(prevInterval);
                    prevInterval = currInterval;
                }
            }
        }
        ans.add(prevInterval);
        return ans.stream().toArray(int[][]::new);
    }
}
```

这代码真丑。

可以优化为：

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        List<int[]> ans = new ArrayList<>();
        int[] prevInterval = intervals[0];
        for (int i = 1; i < intervals.length; i++) {
            int[] currInterval = intervals[i];
            if (prevInterval[1] >= currInterval[0]) {
                prevInterval[1] = Math.max(prevInterval[1], currInterval[1]);
            } else {
                ans.add(prevInterval);
                prevInterval = currInterval;
            }
        }
        ans.add(prevInterval);
        return ans.toArray(new int[ans.size()][]);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n \log n)$

空间复杂度：$O(n)$
