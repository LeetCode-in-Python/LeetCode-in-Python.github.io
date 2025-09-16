[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 54\. Spiral Matrix

Medium

Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

**Input:** matrix = \[\[1,2,3],[4,5,6],[7,8,9]]

**Output:** [1,2,3,6,9,8,7,4,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

**Input:** matrix = \[\[1,2,3,4],[5,6,7,8],[9,10,11,12]]

**Output:** [1,2,3,4,8,12,11,10,9,5,6,7] 

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 10`
*   `-100 <= matrix[i][j] <= 100`

## Solution

```python
from typing import List

class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result = []
        r = 0
        c = 0
        big_r = len(matrix) - 1
        big_c = len(matrix[0]) - 1
        while r <= big_r and c <= big_c:
            for i in range(c, big_c + 1):
                result.append(matrix[r][i])
            r += 1
            for i in range(r, big_r + 1):
                result.append(matrix[i][big_c])
            big_c -= 1
            if r <= big_r:
                for i in range(big_c, c - 1, -1):
                    result.append(matrix[big_r][i])
                big_r -= 1
            if c <= big_c:
                for i in range(big_r, r - 1, -1):
                    result.append(matrix[i][c])
                c += 1
        return result
```