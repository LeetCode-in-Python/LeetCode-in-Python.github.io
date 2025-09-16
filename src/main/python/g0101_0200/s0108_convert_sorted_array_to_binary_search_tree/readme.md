[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 108\. Convert Sorted Array to Binary Search Tree

Easy

Given an integer array `nums` where the elements are sorted in **ascending order**, convert _it to a **height-balanced** binary search tree_.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

**Input:** nums = [-10,-3,0,5,9]

**Output:** [0,-3,9,-10,null,5]

**Explanation:** [0,-10,5,null,-3,null,9] is also accepted: ![](https://assets.leetcode.com/uploads/2021/02/18/btree2.jpg) 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/18/btree.jpg)

**Input:** nums = [1,3]

**Output:** [3,1]

**Explanation:** [1,3] and [3,1] are both a height-balanced BSTs. 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `nums` is sorted in a **strictly increasing** order.

## Solution

```python
from typing import List, Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        # Set up recursion
        return self._makeTree(nums, 0, len(nums) - 1)

    def _makeTree(self, nums: List[int], left: int, right: int) -> Optional[TreeNode]:
        # left as lowest# can't be greater than right
        if left > right:
            return None
        # Set median# as node
        mid = (left + right) // 2
        mid_node = TreeNode(nums[mid])
        # Set mid node's kids
        mid_node.left = self._makeTree(nums, left, mid - 1)
        mid_node.right = self._makeTree(nums, mid + 1, right)
        # Sends node back || Goes back to prev node
        return mid_node
```