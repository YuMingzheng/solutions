---
title: 141. 环形链表
date: 2025-01-17
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/linked-list-cycle/description/)

判断一个单链表中有没有环。

### 解题思路

#### 方法一

使用快慢指针的方法：一个指针每次走一步，另一个每次走两步。如果快指针先走到 `null`，则说明链表中没有环；而如果两个指针相遇，则说明链表中存在环。就好比在操场上跑步，速度快的跑者一定会赶上速度慢的跑者——除非是在马拉松中，快跑者已经提前冲过终点，去到别处了。

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
