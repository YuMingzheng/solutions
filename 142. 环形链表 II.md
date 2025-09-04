---
title: 142. 环形链表 II
date: 2025-01-17
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/linked-list-cycle-ii/description/)

判断一个链表有没有环，如果有，返回环的入口。

### 解题思路

#### 方法一

使用快慢指针的方法：慢指针每次走一步，快指针每次走两步。当快慢指针相遇时，从相遇点开始，再使用一个新的慢指针从起点出发，两个指针每次同时走一步。当这两个慢指针再次相遇时，那个相遇的地方就是环的入口。别问为什么，记住这个方法即可。

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) {
            return null;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                ListNode slow2 = head;
                while (slow != slow2) {
                    slow = slow.next;
                    slow2 = slow2.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
