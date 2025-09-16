[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 82\. Remove Duplicates from Sorted List II

Medium

Given the `head` of a sorted linked list, _delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list_. Return _the linked list **sorted** as well_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

**Input:** head = [1,2,3,3,4,4,5]

**Output:** [1,2,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

**Input:** head = [1,1,1,2,3]

**Output:** [2,3] 

**Constraints:**

*   The number of nodes in the list is in the range `[0, 300]`.
*   `-100 <= Node.val <= 100`
*   The list is guaranteed to be **sorted** in ascending order.

## Solution

```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head
        dummy = ListNode(0)
        prev = dummy
        prev.next = head
        curr = head.next
        while curr is not None:
            flag_found_duplicate = False
            while curr is not None and prev.next.val == curr.val:
                flag_found_duplicate = True
                curr = curr.next
            if flag_found_duplicate:
                prev.next = curr
                if curr is not None:
                    curr = curr.next
            else:
                prev = prev.next
                prev.next = curr
                curr = curr.next
        return dummy.next
```