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

[19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # 双指针解法
        p1, p2 = head, head
        # p2先走k步，当p2此时为空指针时表示n==链表长度，删除头节点
        for i in range(n):
            p2 = p2.next
            if not p2:
                return head.next
        
        # 接着p2到达最后一个节点时，p1到达需删除节点的前一个节点
        while p2.next:
            p1 = p1.next
            p2 = p2.next

        p1.next = p1.next.next

        return head



```
