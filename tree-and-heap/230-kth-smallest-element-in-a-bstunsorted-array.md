# Kth Smallest Element in a BST

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

```py
class TreeNode:
     def __init__(self, x):
         self.val = x
         self.left = None
         self.right = None

class Solution:
    # @param {TreeNode} root
    # @param {integer} k
    # @return {integer}
    def kthSmallest(self, root, k):
        stack = []
        node = root
        while node:
            stack.append(node)
            node = node.left
        x = 1
        while stack and x <= k:
            node = stack.pop()
            x += 1
            right = node.right
            while right:
                stack.append(right)
                right = right.left
        return node.val
```

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

如果BST节点TreeNode的属性可以扩展，则再添加一个属性leftCnt，记录左子树的节点个数
```
记当前节点为node

当node不为空时循环：

若k == node.leftCnt + 1：则返回node

否则，若k > node.leftCnt：则令k -= node.leftCnt + 1，令node = node.right

否则，node = node.left
```
上述算法时间复杂度为O(BST的高度)



---
```py
from heapq import heappush, heappop
class Solution:
    """
    @param: k: An integer
    @param: nums: An integer array
    @return: kth smallest element
    """
    def kthSmallest(self, k, nums):
        max_heap = []
        for num in nums:
            heappush(max_heap, -num)
            if len(max_heap) > k:
                heappop(max_heap)
        
        return - max_heap[0]
```