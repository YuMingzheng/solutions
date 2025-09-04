---
title: 104. 二叉树的最大深度
date: 2025-01-22
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/)

二叉树的深度：从根节点到最远叶子节点的路径长度。

### 解题思路

#### 方法一

用层序遍历，每层计数。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int ans = 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int nLevelNodes = queue.size();
            ans++;
            while (nLevelNodes-- > 0) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$

#### 方法二

用递归。

$二叉树的高度 = Max(左子树的高度, 右子树高度) + 1$。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$

