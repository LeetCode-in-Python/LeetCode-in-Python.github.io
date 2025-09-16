[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 130\. Surrounded Regions

Medium

Given an `m x n` matrix `board` containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by_ `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

**Input:** board = \[\["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

**Output:** [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

**Explanation:** Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically. 

**Example 2:**

**Input:** board = \[\["X"]]

**Output:** [["X"]] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 200`
*   `board[i][j]` is `'X'` or `'O'`.

## Solution

```python
from typing import List

class Solution:
    def solve(self, board: List[List[str]]) -> None:
        # Edge case, empty grid
        if not board:
            return
        # Traverse first and last rows (boundaries)
        for i in range(len(board[0])):
            # first row
            if board[0][i] == 'O':
                # It will convert O and all it's touching O's to #
                self._dfs(board, 0, i)
            # last row
            if board[len(board) - 1][i] == 'O':
                # Converts O's to #'s (same thing as above)
                self._dfs(board, len(board) - 1, i)
        # Traverse first and last Column (boundaries)
        for i in range(len(board)):
            # first Column
            if board[i][0] == 'O':
                # Converts O's to #'s
                self._dfs(board, i, 0)
            # last Column
            if board[i][len(board[0]) - 1] == 'O':
                # Converts O's to #'s
                self._dfs(board, i, len(board[0]) - 1)
        # Traverse through entire matrix
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == 'O':
                    # Convert O's to X's
                    board[i][j] = 'X'
                if board[i][j] == '#':
                    # Convert #'s to O's
                    board[i][j] = 'O'

    def _dfs(self, board: List[List[str]], row: int, column: int):
        if (row < 0 or row >= len(board) or column < 0 or 
            column >= len(board[0]) or board[row][column] != 'O'):
            return
        board[row][column] = '#'
        self._dfs(board, row + 1, column)
        self._dfs(board, row - 1, column)
        self._dfs(board, row, column + 1)
        self._dfs(board, row, column - 1)
```