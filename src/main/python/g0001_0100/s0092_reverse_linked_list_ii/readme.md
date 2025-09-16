[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 92\. Reverse Linked List II

Medium

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

**Input:** head = [1,2,3,4,5], left = 2, right = 4

**Output:** [1,4,3,2,5] 

**Example 2:**

**Input:** head = [5], left = 1, right = 1

**Output:** [5] 

**Constraints:**

*   The number of nodes in the list is `n`.
*   `1 <= n <= 500`
*   `-500 <= Node.val <= 500`
*   `1 <= left <= right <= n`

**Follow up:** Could you do it in one pass?

## Solution

```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        if left == right:
            return head
        prev = None
        temp = head
        start = None
        k = left
        while temp is not None and k > 1:
            prev = temp
            temp = temp.next
            k -= 1
        if left > 1 and prev is not None:
            prev.next = None
        prev1 = None
        start = temp
        while temp is not None and right - left >= 0:
            prev1 = temp
            temp = temp.next
            right -= 1
        if prev1 is not None:
            prev1.next = None
        if left > 1 and prev is not None:
            prev.next = self._reverse(start)
        else:
            head = self._reverse(start)
            prev = head
        while prev.next is not None:
            prev = prev.next
        prev.next = temp
        return head

    def _reverse(self, head: Optional[ListNode]) -> Optional[ListNode]:
        p = head
        r = None
        while p is not None:
            q = p.next
            p.next = r
            r = p
            p = q
        return r
```