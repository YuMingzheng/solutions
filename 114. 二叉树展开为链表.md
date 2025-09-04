---
title: 114. 二叉树展开为链表
date: 2025-02-25
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/description/)

把一个二叉树转化为链表。

### 解题思路

#### 方法一

后序遍历一棵树时，首先访问右子树，再访问左子树，最后访问根节点。在遍历过程中，记录上一次访问的节点，并将当前节点的左子节点设为 `null`，右子节点指向上一次访问的节点。

```java
class Solution {
    private TreeNode prevNode;

    public void flatten(TreeNode node) {
        if (node == null) {
            return;
        }
        flatten(node.right);
        flatten(node.left);
        node.left = null;
        node.right = prevNode;
        prevNode = node;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$

#### 方法二

将左子树转化为链表后的尾节点与右子树转化为链表后的头节点连接，然后将当前节点的右指针指向左链表的头节点。最后返回组成链表的尾节点。有右返回右，有左返回左，都没有返回自己。

```java
class Solution {
    public void flatten(TreeNode root) {
        flatten2(root);
    }

    private TreeNode flatten2(TreeNode node) {
        if (node == null) {
            return null;
        }
        TreeNode leftTail = flatten2(node.left);
        TreeNode rightTail = flatten2(node.right);
        if (leftTail != null) {
            leftTail.right = node.right;
            node.right = node.left;
            node.left = null;
        }
        return rightTail != null ? rightTail : leftTail != null ? leftTail : node;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$
