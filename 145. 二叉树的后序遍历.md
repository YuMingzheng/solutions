---
title: 145. 二叉树的后序遍历
date: 2025-01-21
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/binary-tree-postorder-traversal/description/)

后序遍历一颗树：左子树 -> 右子树 -> 根节点。

### 解题思路

#### 方法一

递归法。

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        postorderTraversal(root, ans);
        return ans;
    }

    public void postorderTraversal(TreeNode node, List<Integer> ans) {
        if (node == null) {
            return;
        }
        postorderTraversal(node.left, ans);
        postorderTraversal(node.right, ans);
        ans.add(node.val);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$

#### 方法二

用栈模拟递归。

在遍历过程中采用 **先左后右的入栈顺序**：如果当前节点存在左子节点，则先将左子节点压入栈；若存在右子节点，再将右子节点压入栈。由于栈的后进先出（LIFO）特性，右子节点会先出栈并被处理，从而保证右子树优先于左子树进行遍历。最终，由于整个遍历顺序为“根-右-左”，通过反转结果列表 `ans`，可以将其调整为符合后序遍历要求的“左-右-根”顺序。

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            ans.add(node.val);
            if (node.left != null) {
                stack.push(node.left);
            }
            if (node.right != null) {
                stack.push(node.right);
            }
        }
        Collections.reverse(ans);
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$

