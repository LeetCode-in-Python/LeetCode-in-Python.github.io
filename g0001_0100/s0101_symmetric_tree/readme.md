101\. Symmetric Tree

Easy

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

**Input:** root = [1,2,2,3,4,4,3]

**Output:** true 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

**Input:** root = [1,2,2,null,3,null,3]

**Output:** false 

**Constraints:**

*   The number of nodes in the tree is in the range `[1, 1000]`.
*   `-100 <= Node.val <= 100`

**Follow up:** Could you solve it both recursively and iteratively?

To solve this task using Python with a `Solution` class, you can follow these steps:

1. Define a class named `Solution`.
2. Inside the class, define a method named `isSymmetric` that takes `root` as an input parameter.
3. Implement an algorithm to check whether the given binary tree is symmetric.
4. Use a recursive approach to check if the left and right subtrees are mirrors of each other.
5. Define a helper function named `isMirror` that takes two nodes `left` and `right` as input parameters.
6. If both `left` and `right` are None, return True (base case).
7. If either `left` or `right` is None, or their values are not equal, return False.
8. Recursively call `isMirror` with `left.left` and `right.right`, and with `left.right` and `right.left`.
9. Return the result of the `isMirror` function for the root's left and right subtrees.

Here's the implementation:

```python
class Solution:
    def isSymmetric(self, root):
        def isMirror(left, right):
            if not left and not right:
                return True
            if not left or not right or left.val != right.val:
                return False
            return isMirror(left.left, right.right) and isMirror(left.right, right.left)
        
        if not root:
            return True
        
        return isMirror(root.left, root.right)

# Example usage:
solution = Solution()
root1 = TreeNode(1)
root1.left = TreeNode(2)
root1.right = TreeNode(2)
root1.left.left = TreeNode(3)
root1.left.right = TreeNode(4)
root1.right.left = TreeNode(4)
root1.right.right = TreeNode(3)
print(solution.isSymmetric(root1))  # Output: True

root2 = TreeNode(1)
root2.left = TreeNode(2)
root2.right = TreeNode(2)
root2.left.right = TreeNode(3)
root2.right.right = TreeNode(3)
print(solution.isSymmetric(root2))  # Output: False
```

This solution checks whether the given binary tree is symmetric by comparing its left and right subtrees. It has a time complexity of O(n), where n is the number of nodes in the tree, as it traverses each node exactly once.