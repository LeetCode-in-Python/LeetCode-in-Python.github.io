114\. Flatten Binary Tree to Linked List

Medium

Given the `root` of a binary tree, flatten the tree into a "linked list":

*   The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
*   The "linked list" should be in the same order as a [**pre-order** **traversal**](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

**Input:** root = [1,2,5,3,4,null,6]

**Output:** [1,null,2,null,3,null,4,null,5,null,6] 

**Example 2:**

**Input:** root = []

**Output:** [] 

**Example 3:**

**Input:** root = [0]

**Output:** [0] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-100 <= Node.val <= 100`

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

To solve this task, we can use a recursive approach to flatten the binary tree. We'll define a `Solution` class with a method `flatten` to perform this task. Here are the steps:

1. Define the `Solution` class.
2. Define the `flatten` method which takes `root` as input.
3. Create a helper function, let's call it `flattenHelper`, that takes a node as input.
4. In the `flattenHelper` function, if the current node is `None`, return `None`.
5. Otherwise, recursively flatten the left subtree and right subtree.
6. Once both subtrees are flattened, set the `right` child of the root to the flattened left subtree.
7. Traverse to the end of the flattened left subtree and attach the flattened right subtree to its `right`.
8. Set the `left` child of the root to `None`.
9. Return the last node of the flattened tree (either the last node of the flattened right subtree or the last node of the flattened left subtree if the right subtree is `None`).
10. Call `flattenHelper` from the `flatten` method with the root node.
11. Return the root node.

Here's the Python code implementing these steps:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def flatten(self, root):
        def flattenHelper(node):
            if not node:
                return None
            
            left_last = flattenHelper(node.left)
            right_last = flattenHelper(node.right)
            
            if left_last:
                left_last.right = node.right
                node.right = node.left
                node.left = None
            
            return right_last if right_last else left_last if left_last else node
        
        flattenHelper(root)
        return root
```

You can then use this `Solution` class to flatten the binary tree into a linked list in pre-order traversal order.