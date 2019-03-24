### 题目描述

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
partiton，运行一直超时
```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        if not tinput or k <= 0 or k > len(tinput):
            return []
        
        left, right = 0, len(tinput) - 1
        index = self.partiton(tinput, left, right)
        while k - 1 != index:
            if k - 1 < index:
                index = self.partiton(tinput, left, index - 1)
            else:
                index = self.partiton(tinput, index + 1, right)

        return tinput[:k]

    def partiton(self, array, left, right):
        pivot = array[left]
        while left < right:
            while left < right and array[right] > pivot:
                right -= 1
            array[left] = array[right]

            while left < right and array[left] <= pivot:
                left += 1
            array[right] = array[left]
        array[left] = pivot

        return left

```
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
        return tinput[:k]

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

```
