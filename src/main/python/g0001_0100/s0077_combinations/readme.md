[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 77\. Combinations

Medium

Given two integers `n` and `k`, return _all possible combinations of_ `k` _numbers out of the range_ `[1, n]`.

You may return the answer in **any order**.

**Example 1:**

**Input:** n = 4, k = 2

**Output:** [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ] 

**Example 2:**

**Input:** n = 1, k = 1

**Output:** [[1]] 

**Constraints:**

*   `1 <= n <= 20`
*   `1 <= k <= n`

## Solution

```python
from typing import List

class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        ans = []
        # Boundary case
        if n > 20 or k < 1 or k > n:
            return ans
        self._backtrack(ans, n, k, 1, [])
        return ans

    def _backtrack(self, ans: List[List[int]], n: int, k: int, s: int, stack: List[int]):
        # Base case
        # If k becomes 0
        if k == 0:
            ans.append(stack[:])
            return
        # Start with s till n-k+1
        for i in range(s, n - k + 2):
            stack.append(i)
            # Update start for recursion and decrease k by 1
            self._backtrack(ans, n, k - 1, i + 1, stack)
            stack.pop()
```