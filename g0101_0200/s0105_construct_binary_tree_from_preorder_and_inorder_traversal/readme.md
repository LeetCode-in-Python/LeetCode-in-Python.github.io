105\. Construct Binary Tree from Preorder and Inorder Traversal

Medium

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

**Output:** [3,9,20,null,null,15,7] 

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]

**Output:** [-1] 

**Constraints:**

*   `1 <= preorder.length <= 3000`
*   `inorder.length == preorder.length`
*   `-3000 <= preorder[i], inorder[i] <= 3000`
*   `preorder` and `inorder` consist of **unique** values.
*   Each value of `inorder` also appears in `preorder`.
*   `preorder` is **guaranteed** to be the preorder traversal of the tree.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.

To solve this task, we can use a recursive approach to construct the binary tree. We'll define a `Solution` class with a method `buildTree` to perform this task. Here are the steps:

1. Define the `Solution` class.
2. Define the `buildTree` method which takes `preorder` and `inorder` lists as input.
3. Create a helper function, let's call it `buildTreeHelper`, that takes the indices representing the current subtree in preorder and inorder lists.
4. In the `buildTreeHelper` function, if the `preorder` list is empty or the `inorder` list is empty, return `None`, indicating an empty subtree.
5. Otherwise, the first element of the `preorder` list would be the root of the current subtree. Create a node for this root.
6. Find the index of the root value in the `inorder` list. This index will partition the `inorder` list into left and right subtrees.
7. Recursively call `buildTreeHelper` for the left subtree with appropriate indices.
8. Recursively call `buildTreeHelper` for the right subtree with appropriate indices.
9. Return the root node.
10. Call `buildTreeHelper` from the `buildTree` method with initial indices for the entire preorder and inorder lists.
11. Return the root node obtained from `buildTreeHelper`.

Here's the Python code implementing these steps:

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def buildTree(self, preorder, inorder):
        if not preorder or not inorder:
            return None
        
        def buildTreeHelper(pre_start, pre_end, in_start, in_end):
            if pre_start > pre_end or in_start > in_end:
                return None
            
            root_val = preorder[pre_start]
            root = TreeNode(root_val)
            
            # Find index of root value in inorder list
            root_index = inorder.index(root_val)
            
            # Calculate the number of nodes in the left subtree
            left_subtree_size = root_index - in_start
            
            # Recursively build left subtree
            root.left = buildTreeHelper(pre_start + 1, pre_start + left_subtree_size, in_start, root_index - 1)
            
            # Recursively build right subtree
            root.right = buildTreeHelper(pre_start + left_subtree_size + 1, pre_end, root_index + 1, in_end)
            
            return root
        
        return buildTreeHelper(0, len(preorder) - 1, 0, len(inorder) - 1)
```

You can then use this `Solution` class to construct the binary tree from preorder and inorder traversal arrays.