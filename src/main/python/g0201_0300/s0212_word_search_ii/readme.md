[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 212\. Word Search II

Hard

Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

**Input:** board = \[\["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]

**Output:** ["eat","oath"] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)

**Input:** board = \[\["a","b"],["c","d"]], words = ["abcb"]

**Output:** [] 

**Constraints:**

*   `m == board.length`
*   `n == board[i].length`
*   `1 <= m, n <= 12`
*   `board[i][j]` is a lowercase English letter.
*   <code>1 <= words.length <= 3 * 10<sup>4</sup></code>
*   `1 <= words[i].length <= 10`
*   `words[i]` consists of lowercase English letters.
*   All the strings of `words` are unique.

## Solution

```python
from typing import List

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        alphabets = [chr(ord("a") + i) for i in range(26)] + ["end"]
        trie = {i:None for i in alphabets}
        for word in words:
            root = trie
            for letter in word:
                if not root[letter]: 
                    root[letter] = {i:None for i in alphabets}
                root = root[letter]
            root["end"] = True

        y, x = len(board), len(board[0])
        visited = [[False]*x for _ in range(y)]
        ans = []

        def remove_word(word, root = trie):
            if word: root[word[0]] = remove_word(word[1:], root[word[0]])

            for i in root:
                if root[i]: return root
                
            return None
        
        def getAns(m, n, root, word):

            if root["end"]: 
                ans.append(word)
                root["end"] = False
                remove_word(word)

            visited[m][n] = True
            for i,j in [[1,0],[-1,0],[0,1],[0,-1]]:
                a, b = m+i, n+j
                if 0 <= a < y and 0 <= b < x and visited[a][b] == False and root[board[a][b]]:
                    getAns(a, b, root[board[a][b]], word + board[a][b])
            visited[m][n] = False

            return

        for i in range(y):
            for j in range(x):
                if trie[board[i][j]]:
                    getAns(i, j, trie[board[i][j]], board[i][j])
        
        return ans
```