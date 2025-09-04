---
title: 19. 删除链表的倒数第 N 个结点
date: 2025-01-14
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/description/)

从链表末尾往前数，删除第 n 个节点。

### 解题思路

#### 方法一

添加一个虚拟的哨兵节点，即使删除的是链表的头节点，操作逻辑也与删除中间节点完全一致。始终让 `left.next` 指向要删除的节点。

具体步骤如下：

1. 让右指针先向右移动 `n` 步，以确保左右指针之间的距离为 `n`。
2. 然后同时移动左右指针，直到右指针到达链表末尾。
3. 此时，左指针 `left` 的 `next` 指针直接跳过目标节点，将其从链表中移除。

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode sentinelNode = new ListNode(Integer.MAX_VALUE, head);
        ListNode left = sentinelNode;
        ListNode right = sentinelNode;
        while (right.next != null) {
            right = right.next;
            if (--n < 0) {
                left = left.next;
            }
        }
        left.next = left.next.next;
        return sentinelNode.next;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
