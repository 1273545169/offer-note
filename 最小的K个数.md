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
运行一直超时
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
