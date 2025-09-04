---
title: 160. 相交链表
date: 2025-01-14
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/intersection-of-two-linked-lists/description/)

找到两个链表相交的那个节点。

### 解题思路

#### 方法一

`headA` 从起点开始向后遍历，到达末尾后转到 `headB` 的起点继续遍历；同样，`headB` 从起点开始向后遍历，到达末尾后转到 `headA` 的起点继续遍历。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode startA = headA;
        ListNode startB = headB;
        boolean isAShifted = false;
        boolean isBShifted = false;
        while (headA != null || headB != null) {
            if (headA == headB) {
                return headA;
            }
            if (!isAShifted && headA.next == null) {
                headA = startB;
                isAShifted = true;
            } else if (headA != null) {
                headA = headA.next;
            }
            if (!isBShifted && headB.next == null) {
                headB = startA;
                isBShifted = true;
            } else if (headB != null) {
                headB = headB.next;
            }
        }
        return null;
    }
}
```

`headA` 和 `headB` 走的步数相同，如果不相交，最后都会到达 `null`。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode ptrA = headA;
        ListNode ptrB = headB;
        while (ptrA != ptrB) {
            ptrA = (ptrA == null) ? headB : ptrA.next;
            ptrB = (ptrB == null) ? headA : ptrB.next;
        }
        return ptrA;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(m + n)$

空间复杂度：$O(1)$
