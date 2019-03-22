### 题目描述

输入一个链表，输出该链表中倒数第k个结点。

### 思路解析

考虑三个临界点：`若k<=0；若链表为空；若链表长度小于k`

p1先走k-1步，从第k步开始，p1和p2同时走，p1走到最后一个位置时，p2正好在倒数第k个位置，返回p2指的节点

```python

class Solution:
    def FindKthToTail(self, head, k):
        if not head or not k:
            return None

        p1, p2 = head, head
        # p1先走k-1步
        for i in range(k - 1):
            p1 = p1.next
            if not p1:
                return None
        # p1和p2同时走，p1走到最后一个位置时，p2正好在倒数第k个位置，返回p2指的节点
        while p1.next:
            p1 = p1.next
            p2 = p2.next
        return p2

```
万能的list结构，时间稍长一点

```python

class Solution:
    def FindKthToTail(self, head, k):
        if k <= 0:
            return None
        res = []
        while head:
            res.append(head)
            head = head.next

        return res[-k] if len(res) >= k else None

```
