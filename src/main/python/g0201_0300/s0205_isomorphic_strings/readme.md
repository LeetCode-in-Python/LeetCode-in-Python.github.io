[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 205\. Isomorphic Strings

Easy

Given two strings `s` and `t`, _determine if they are isomorphic_.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

**Input:** s = "egg", t = "add"

**Output:** true 

**Example 2:**

**Input:** s = "foo", t = "bar"

**Output:** false 

**Example 3:**

**Input:** s = "paper", t = "title"

**Output:** true 

**Constraints:**

*   <code>1 <= s.length <= 5 * 10<sup>4</sup></code>
*   `t.length == s.length`
*   `s` and `t` consist of any valid ascii character.

## Solution

```python
from typing import List

class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        map_array = [0] * 128
        str_chars = list(s)
        tar_chars = list(t)
        n = len(str_chars)
        for i in range(n):
            if map_array[ord(tar_chars[i])] == 0:
                if self._search(map_array, ord(str_chars[i]), ord(tar_chars[i])) != -1:
                    return False
                map_array[ord(tar_chars[i])] = ord(str_chars[i])
            else:
                if map_array[ord(tar_chars[i])] != ord(str_chars[i]):
                    return False
        return True

    def _search(self, map_array: List[int], target: int, skip: int) -> int:
        for i in range(128):
            if i == skip:
                continue
            if map_array[i] != 0 and map_array[i] == target:
                return i
        return -1
```