### 题目描述

[二叉搜索树的第k个节点](https://www.nowcoder.com/practice/ef068f602dde4d28aab2b210e859150a?tpId=13&tqId=11215&tPage=4&rp=2&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)


### 思路解析

```python

class Solution:
    # 返回对应节点TreeNode
    def KthNode(self, root, k):
        if not root:
            return root

        stack = []
        cnt = 0
        while root or stack:
            if root:
                stack.append(root)
                root = root.left
            else:
                root = stack.pop()
                cnt += 1
                if cnt == k:
                    return root
                root = root.right

```
