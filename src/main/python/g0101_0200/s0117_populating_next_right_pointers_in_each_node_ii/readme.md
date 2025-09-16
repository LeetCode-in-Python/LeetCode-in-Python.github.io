[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 117\. Populating Next Right Pointers in Each Node II

Medium

Given a binary tree

struct Node { int val; Node \*left; Node \*right; Node \*next; } 

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

**Input:** root = [1,2,3,4,5,null,7]

**Output:** [1,#,2,3,#,4,5,7,#]

**Explanation:** Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level. 

**Example 2:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 6000]`.
*   `-100 <= Node.val <= 100`

**Follow-up:**

*   You may only use constant extra space.
*   The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

## Solution

```python
from typing import Optional

class Node:
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next

class Solution:
    def connect(self, root: Optional[Node]) -> Optional[Node]:
        if root is None:
            return None
        if root.left is None and root.right is None:
            return root
        if root.left is not None:
            if root.right is not None:
                root.left.next = root.right
            elif root.next is not None:
                root.left.next = self._adjacentRightNode(root.next)
        if root.right is not None:
            root.right.next = self._adjacentRightNode(root.next)
        self.connect(root.right)
        self.connect(root.left)
        return root

    def _adjacentRightNode(self, root: Optional[Node]) -> Optional[Node]:
        temp = root
        while temp is not None:
            if temp.left is None and temp.right is None:
                temp = temp.next
            else:
                if temp.left is not None:
                    return temp.left
                if temp.right is not None:
                    return temp.right
        return None
```