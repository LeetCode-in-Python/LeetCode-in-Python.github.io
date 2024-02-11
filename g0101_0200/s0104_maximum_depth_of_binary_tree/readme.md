104\. Maximum Depth of Binary Tree

Easy

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** 3 

**Example 2:**

**Input:** root = [1,null,2]

**Output:** 2 

**Example 3:**

**Input:** root = []

**Output:** 0 

**Example 4:**

**Input:** root = [0]

**Output:** 1 

**Constraints:**

*   The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.
*   `-100 <= Node.val <= 100`

To solve this task using Python with a `Solution` class, you can follow these steps:

1. Define a class named `Solution`.
2. Inside the class, define a method named `maxDepth` that takes `root` as an input parameter.
3. Implement an algorithm to calculate the maximum depth of the binary tree.
4. Use a recursive approach to traverse the tree and calculate the depth.
5. Define a helper function named `calculateDepth` that takes a node as an input parameter and returns its depth.
6. If the node is None, return 0 (base case).
7. Recursively calculate the depth of the left and right subtrees.
8. Return the maximum of the depths of the left and right subtrees, plus 1 (to account for the current node).
9. Call the `calculateDepth` function with the root node to get the maximum depth of the binary tree.

Here's the implementation:

```python
class Solution:
    def maxDepth(self, root):
        def calculateDepth(node):
            if not node:
                return 0
            return max(calculateDepth(node.left), calculateDepth(node.right)) + 1
        
        return calculateDepth(root)

# Example usage:
solution = Solution()
root = TreeNode(3)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)
print(solution.maxDepth(root))  # Output: 3
```

This solution calculates the maximum depth of the binary tree using a recursive approach. It has a time complexity of O(n), where n is the number of nodes in the tree, as it traverses each node exactly once.