[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 97\. Interleaving String

Medium

Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an **interleaving** of `s1` and `s2`.

An **interleaving** of two strings `s` and `t` is a configuration where they are divided into **non-empty** substrings such that:

*   <code>s = s<sub>1</sub> + s<sub>2</sub> + ... + s<sub>n</sub></code>
*   <code>t = t<sub>1</sub> + t<sub>2</sub> + ... + t<sub>m</sub></code>
*   `|n - m| <= 1`
*   The **interleaving** is <code>s<sub>1</sub> + t<sub>1</sub> + s<sub>2</sub> + t<sub>2</sub> + s<sub>3</sub> + t<sub>3</sub> + ...</code> or <code>t<sub>1</sub> + s<sub>1</sub> + t<sub>2</sub> + s<sub>2</sub> + t<sub>3</sub> + s<sub>3</sub> + ...</code>

**Note:** `a + b` is the concatenation of strings `a` and `b`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

**Input:** s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"

**Output:** true 

**Example 2:**

**Input:** s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"

**Output:** false 

**Example 3:**

**Input:** s1 = "", s2 = "", s3 = ""

**Output:** true 

**Constraints:**

*   `0 <= s1.length, s2.length <= 100`
*   `0 <= s3.length <= 200`
*   `s1`, `s2`, and `s3` consist of lowercase English letters.

**Follow up:** Could you solve it using only `O(s2.length)` additional memory space?

## Solution

```python
from typing import List, Optional

class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s3) != (len(s1) + len(s2)):
            return False
        cache: List[List[Optional[bool]]] = [[None for _ in range(len(s2) + 1)] for _ in range(len(s1) + 1)]
        return self._isInterleave(s1, s2, s3, 0, 0, 0, cache)

    def _isInterleave(self, s1: str, s2: str, s3: str, i1: int, i2: int, i3: int, cache: List[List[Optional[bool]]]) -> bool:
        if cache[i1][i2] is not None:
            return cache[i1][i2]
        if i1 == len(s1) and i2 == len(s2) and i3 == len(s3):
            return True
        result = False
        if i1 < len(s1) and s1[i1] == s3[i3]:
            result = self._isInterleave(s1, s2, s3, i1 + 1, i2, i3 + 1, cache)
        if i2 < len(s2) and s2[i2] == s3[i3]:
            result = result or self._isInterleave(s1, s2, s3, i1, i2 + 1, i3 + 1, cache)
        cache[i1][i2] = result
        return result
```