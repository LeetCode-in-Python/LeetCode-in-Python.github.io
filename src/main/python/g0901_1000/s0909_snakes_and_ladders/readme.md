[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 909\. Snakes and Ladders

Medium

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to <code>n<sup>2</sup></code> in a [**Boustrophedon style**](https://en.wikipedia.org/wiki/Boustrophedon) starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:

*   Choose a destination square `next` with a label in the range <code>[curr + 1, min(curr + 6, n<sup>2</sup>)]</code>.
    *   This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.
*   If `next` has a snake or ladder, you **must** move to the destination of that snake or ladder. Otherwise, you move to `next`.
*   The game ends when you reach the square <code>n<sup>2</sup></code>.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and <code>n<sup>2</sup></code> do not have a snake or ladder.

Note that you only take a snake or ladder at most once per move. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** follow the subsequent snake or ladder.

*   For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square `3`, but do **not** follow the subsequent ladder to `4`.

Return _the least number of moves required to reach the square_ <code>n<sup>2</sup></code>_. If it is not possible to reach the square, return_ `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/09/23/snakes.png)

**Input:** board = \[\[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]

**Output:** 4

**Explanation:** 

In the beginning, you start at square 1 (at row 5, column 0). 

You decide to move to square 2 and must take the ladder to square 15. 

You then decide to move to square 17 and must take the snake to square 13. 

You then decide to move to square 14 and must take the ladder to square 35. 

You then decide to move to square 36, ending the game. 

This is the lowest possible number of moves to reach the last square, so return 4.

**Example 2:**

**Input:** board = \[\[-1,-1],[-1,3]]

**Output:** 1

**Constraints:**

*   `n == board.length == board[i].length`
*   `2 <= n <= 20`
*   `grid[i][j]` is either `-1` or in the range <code>[1, n<sup>2</sup>]</code>.
*   The squares labeled `1` and <code>n<sup>2</sup></code> do not have any ladders or snakes.

## Solution

```python
from collections import deque
from typing import List

class Solution:
    def snakesAndLadders(self, board: List[List[int]]) -> int:
        n = len(board)
        target = n * n
        visited = [False] * target
        queue = deque([1])
        visited[0] = True
        step = 0
        
        while queue:
            queue_size = len(queue)
            for _ in range(queue_size):
                current_label = queue.popleft()
                if current_label == target:
                    return step
                
                for next_label in range(current_label + 1, min(target + 1, current_label + 7)):
                    if visited[next_label - 1]:
                        continue
                    visited[next_label - 1] = True
                    
                    row, col = self.indexToPosition(next_label, n)
                    if board[row][col] == -1:
                        queue.append(next_label)
                    else:
                        queue.append(board[row][col])
            step += 1
        
        return -1
    
    def indexToPosition(self, index: int, n: int) -> tuple:
        vertical = n - 1 - (index - 1) // n
        if (n - vertical) % 2 == 1:
            horizontal = (index - 1) % n
        else:
            horizontal = n - 1 - (index - 1) % n
        return vertical, horizontal
```