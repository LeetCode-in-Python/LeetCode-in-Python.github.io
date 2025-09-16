[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 106\. Construct Binary Tree from Inorder and Postorder Traversal

Medium

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]

**Output:** [3,9,20,null,null,15,7] 

**Example 2:**

**Input:** inorder = [-1], postorder = [-1]

**Output:** [-1] 

**Constraints:**

*   `1 <= inorder.length <= 3000`
*   `postorder.length == inorder.length`
*   `-3000 <= inorder[i], postorder[i] <= 3000`
*   `inorder` and `postorder` consist of **unique** values.
*   Each value of `postorder` also appears in `inorder`.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.
*   `postorder` is **guaranteed** to be the postorder traversal of the tree.

## Solution

```python
from typing import List, Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        in_index = [len(inorder) - 1]
        post_index = [len(postorder) - 1]
        return self._helper(inorder, postorder, in_index, post_index, float('inf'))

    def _helper(self, inorder: List[int], postorder: List[int], index: List[int], p_index: List[int], target: int) -> Optional[TreeNode]:
        if index[0] < 0 or (index[0] < len(inorder) and inorder[index[0]] == target):
            return None
        root = TreeNode(postorder[p_index[0]])
        p_index[0] -= 1
        root.right = self._helper(inorder, postorder, index, p_index, root.val)
        index[0] -= 1
        root.left = self._helper(inorder, postorder, index, p_index, target)
        return root
```