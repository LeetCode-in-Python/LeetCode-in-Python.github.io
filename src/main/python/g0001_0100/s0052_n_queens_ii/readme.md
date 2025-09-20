[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 52\. N-Queens II

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _the number of distinct solutions to the **n-queens puzzle**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** 2

**Explanation:** There are two distinct solutions to the 4-queens puzzle as shown. 

**Example 2:**

**Input:** n = 1

**Output:** 1 

**Constraints:**

*   `1 <= n <= 9`

## Solution

```python
class Solution:
    def totalNQueens(self, n: int) -> int:
        row = [False] * n
        col = [False] * n
        diagonal = [False] * (2 * n - 1)
        antiDiagonal = [False] * (2 * n - 1)
        return self._totalNQueens(n, 0, row, col, diagonal, antiDiagonal)

    def _totalNQueens(self, n, r, row, col, diagonal, antiDiagonal):
        if r == n:
            return 1
        count = 0
        for c in range(n):
            if not row[r] and not col[c] and not diagonal[r + c] and not antiDiagonal[r - c + n - 1]:
                row[r] = col[c] = diagonal[r + c] = antiDiagonal[r - c + n - 1] = True
                count += self._totalNQueens(n, r + 1, row, col, diagonal, antiDiagonal)
                row[r] = col[c] = diagonal[r + c] = antiDiagonal[r - c + n - 1] = False
        return count
```