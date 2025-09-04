---
title: 144. 二叉树的前序遍历
date: 2025-01-21
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/binary-tree-preorder-traversal/description/)

前序遍历一颗树：根节点 -> 左子树 -> 右子树。

### 解题思路

#### 方法一

递归。

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        preorderTraversal(ans, root);
        return ans;
    }

    public void preorderTraversal(List<Integer> ans, TreeNode node) {
        if (node == null) {
            return;
        }
        ans.add(node.val);
        preorderTraversal(ans, node.left);
        preorderTraversal(ans, node.right);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$

#### 方法二

用栈模拟递归。

由于栈的先进后出性质，要把之后访问的元素先添加到栈里。注意 `null` 也算一个元素，会导致栈不为空，所以要先判空再入栈。

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            ans.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$
