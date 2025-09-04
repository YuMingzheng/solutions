---
title: 543. 二叉树的直径
date: 2025-01-24
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/diameter-of-binary-tree/description/)

在树中找到两个节点，使连接它们的路径最长，返回长度。

### 解题思路

#### 方法一：递归

一棵树的最长路径长度等于左子树和右子树的最长路径之和，实际上就是将左右子树的深度相加。

在做递归题时，可以先从叶子节点的上一层小树入手，计算当前小树的最长路径长度，然后将小树的深度返回给上一层进行处理。

```java
class Solution {
    int ans = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        treeDepth(root);
        return ans;
    }

    public int treeDepth(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int leftDepth = treeDepth(node.left);
        int rightDepth = treeDepth(node.right);
        ans = Math.max(ans, leftDepth + rightDepth);
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
