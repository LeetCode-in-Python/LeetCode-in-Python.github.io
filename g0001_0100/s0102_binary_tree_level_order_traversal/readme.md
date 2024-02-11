102\. Binary Tree Level Order Traversal

Medium

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [[3],[9,20],[15,7]] 

**Example 2:**

**Input:** root = [1]

**Output:** [[1]] 

**Example 3:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-1000 <= Node.val <= 1000`

To solve this task using Python with a `Solution` class, you can follow these steps:

1. Define a class named `Solution`.
2. Inside the class, define a method named `levelOrder` that takes `root` as an input parameter.
3. Implement an algorithm to perform a level order traversal of the binary tree.
4. Use a queue-based approach to traverse the tree level by level.
5. Initialize a queue with the root node.
6. While the queue is not empty:
    - Initialize an empty list `level_vals` to store the values of nodes at the current level.
    - Iterate through the nodes in the queue (i.e., the nodes at the current level):
        - Pop the node from the front of the queue.
        - Add the value of the node to `level_vals`.
        - If the node has left and/or right children, enqueue them.
    - Append `level_vals` to the result list.
7. Return the result list containing the level order traversal.

Here's the implementation:

```python
from collections import deque

class Solution:
    def levelOrder(self, root):
        if not root:
            return []
        
        result = []
        queue = deque([root])
        
        while queue:
            level_vals = []
            level_size = len(queue)
            
            for _ in range(level_size):
                node = queue.popleft()
                level_vals.append(node.val)
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            result.append(level_vals)
        
        return result

# Example usage:
solution = Solution()
root = TreeNode(3)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)
print(solution.levelOrder(root))  # Output: [[3], [9, 20], [15, 7]]
```

This solution performs a level order traversal of the binary tree using a queue-based approach. It traverses each node exactly once, resulting in a time complexity of O(n), where n is the number of nodes in the tree.