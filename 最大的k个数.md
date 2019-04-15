### 题目描述

[leetcode 215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/submissions/)升级版

输入n个整数，找出其中最大的K个数。k个数排好序

### 思路解析

```python
import heapq

class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        if not tinput or k <= 0 or k > len(tinput):
            return []
        heap = []
        # 数组前k个数构成一个最小堆
        for i in range(k):
            heapq.heappush(heap, tinput[i])
        # 数组后面的数与堆顶比较，大则替换堆顶，再调整前k个数组成新的最小堆
        for i in range(k, len(tinput)):
            if heap[0] < tinput[i]:
                heapq.heapreplace(heap, tinput[i])
        return self.heapSort(heap)[::-1]

    # 堆排序
    def heapSort(self, array):
        res = []
        for i in range(len(array)):
            heapq.heappush(res, array[i])
        return [heapq.heappop(res) for i in range(len(res))]

```
