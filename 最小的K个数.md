### 题目描述

[牛客链接](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf?tpId=13&tqId=11182&tPage=2&rp=2&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

### 思路解析

先排序再输出

```python

class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        if not tinput or k <= 0 or k > len(tinput):
            return 0
        return sorted(tinput)[:k]

```
partiton

[code](https://github.com/1273545169/Leetcode/blob/master/215%20%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E7%AC%ACK%E4%B8%AA%E6%9C%80%E5%A4%A7%E5%85%83%E7%B4%A0.md)

最大堆

```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        if not tinput or k <= 0 or k > len(tinput):
            return []
        # 数组前k个数构成一个最大堆
        for i in range(k):
            self.heapInsert(tinput, i)
        # 数组后面的数与堆顶比较，小则替换堆顶，再调整前k个数组成新的最大堆
        for i in range(k, len(tinput)):
            if tinput[0] > tinput[i]:
                tinput[0] = tinput[i]
                self.heapify(tinput, 0, k)
        return self.heapSort(tinput[:k])

    def heapInsert(self, tinput, index):
        while index > 0 and tinput[index] > tinput[(index - 1) // 2]:
            tinput[index], tinput[(index - 1) // 2] = tinput[(index - 1) // 2], tinput[index]
            index = (index - 1) // 2

    def heapify(self, tinput, index, heapsize):
        left = index * 2 + 1
        while left < heapsize:
            right = left + 1
            if right < heapsize:
                largest = right if tinput[right] > tinput[left] else left
            else:
                largest = left
            if tinput[index] > tinput[largest]:
                break

            tinput[largest], tinput[index] = tinput[index], tinput[largest]
            index = largest
            left = index * 2 + 1
        return tinput

    def heapSort(self, tinput):
        heapsize = len(tinput)
        while heapsize > 1:
            tinput[0], tinput[heapsize - 1] = tinput[heapsize - 1], tinput[0]
            heapsize -= 1
            self.heapify(tinput, 0, heapsize)
        return tinput

```
使用Python的`heapq`模块实现

heapq为最小堆，为了实现最大堆，只需要将在构建时存为负值即可。

例如：heapq.heappush(heap, -tinput[i])

```python

import heapq
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        if not tinput or k <= 0 or k > len(tinput):
            return []
        heap = []
        # 数组前k个数构成一个最大堆
        for i in range(k):
            heapq.heappush(heap, -tinput[i])
        # 数组后面的数与堆顶比较，小则替换堆顶，再调整前k个数组成新的最大堆
        for i in range(k, len(tinput)):
            if heap[0] < -tinput[i]:
                heap[0] = -tinput[i]
                heapq.heapify(heap)
        return self.heapSort(list(map(abs, heap)))

    # 堆排序
    def heapSort(self, array):
        res = []
        for i in range(len(array)):
            heapq.heappush(res, array[i])
        return [heapq.heappop(res) for i in range(len(res))]

```
