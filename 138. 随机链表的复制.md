---
title: 138. 随机链表的复制
date: 2025-01-15
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/copy-list-with-random-pointer/description/)

实现对链表的深拷贝：新链表的结构和指针关系完全复制了原链表，但每个节点的地址与原链表的地址不同。

### 解题思路

#### 方法一

使用哈希表，首先遍历链表一次，构建一个旧节点到新节点的映射。然后，再次遍历原链表，为新链表的节点建立连接。

```java
class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node, Node> oldToNew = new HashMap<>();

        Node currNode = head;
        while (currNode != null) {
            Node newNode = new Node(currNode.val);
            oldToNew.put(currNode, newNode);
            currNode = currNode.next;
        }

        currNode = head;
        while (currNode != null) {
            Node newNode = oldToNew.get(currNode);
            Node oldNodeNext = currNode.next;
            newNode.next = oldToNew.get(oldNodeNext);
            Node randomNode = currNode.random;
            newNode.random = oldToNew.get(randomNode);
            currNode = currNode.next;
        }

        return oldToNew.get(head);
    }
}
```

#### 方法二

遍历链表三次：第一次将新节点插入到对应旧节点的右侧；第二次为新节点的 `random` 指针建立连接；第三次将新链表与原链表分离。

```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return head;
        }

        Node currNode = head;

        while (currNode != null) {
            Node nextNode = currNode.next;
            Node newNode = new Node(currNode.val);
            newNode.next = nextNode;
            currNode.next = newNode;
            currNode = currNode.next.next;
        }

        Node oldNode = head;
        Node newNode = head.next;
        while (true) {
            Node oldRandom = oldNode.random;
            newNode.random = oldRandom != null ? oldRandom.next : null;

            oldNode = newNode.next;
            if (oldNode == null) {
                break;
            }
            newNode = oldNode.next;
        }

        oldNode = head;
        newNode = head.next;
        Node ans = newNode;
        while (true) {
            oldNode.next = newNode.next;
            if (oldNode.next == null) {
                break;
            }
            newNode.next = newNode.next.next;
            oldNode = oldNode.next;
            newNode = newNode.next;
        }

        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
