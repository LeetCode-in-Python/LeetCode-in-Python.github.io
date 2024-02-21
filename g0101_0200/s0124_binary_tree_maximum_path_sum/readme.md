124\. Binary Tree Maximum Path Sum

Hard

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

**Input:** root = [1,2,3]

**Output:** 6

**Explanation:** The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6. 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

**Input:** root = [-10,9,20,null,null,15,7]

**Output:** 42

**Explanation:** The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42. 

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 3 * 10<sup>4</sup>]</code>.
*   `-1000 <= Node.val <= 1000`

To solve this task, we can use a recursive approach to traverse the binary tree and calculate the maximum path sum. We'll define a `Solution` class with a method `maxPathSum` to perform this task. Here are the steps:

1. Define the `Solution` class.
2. Define the `maxPathSum` method which takes `root` as input.
3. Create a helper function, let's call it `maxPathSumHelper`, that takes a node as input.
4. In the `maxPathSumHelper` function, if the current node is `None`, return `0`.
5. Recursively calculate the maximum path sum for the left and right subtrees using `maxPathSumHelper`.
6. Calculate the maximum path sum passing through the current node, considering the possibility of including both left and right subtrees.
7. Update a global variable `max_sum` to keep track of the maximum path sum encountered so far.
8. Return the maximum path sum that includes either the current node or just one of its subtrees (if the sum with both subtrees is negative).
9. Call `maxPathSumHelper` from the `maxPathSum` method with the root node.
10. Return the global variable `max_sum`.

Here's the Python code implementing these steps:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxPathSum(self, root):
        def maxPathSumHelper(node):
            if not node:
                return 0
            
            left_sum = max(maxPathSumHelper(node.left), 0)
            right_sum = max(maxPathSumHelper(node.right), 0)
            
            current_max = node.val + left_sum + right_sum
            
            global max_sum
            max_sum = max(max_sum, current_max)
            
            return node.val + max(left_sum, right_sum)
        
        max_sum = float('-inf')
        maxPathSumHelper(root)
        return max_sum
```

You can then use this `Solution` class to find the maximum path sum of any non-empty path in the binary tree.