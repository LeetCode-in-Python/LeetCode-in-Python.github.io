[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 290\. Word Pattern

Easy

Given a `pattern` and a string `s`, find if `s` follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in `pattern` and a **non-empty** word in `s`.

**Example 1:**

**Input:** pattern = "abba", s = "dog cat cat dog"

**Output:** true 

**Example 2:**

**Input:** pattern = "abba", s = "dog cat cat fish"

**Output:** false 

**Example 3:**

**Input:** pattern = "aaaa", s = "dog cat cat dog"

**Output:** false 

**Example 4:**

**Input:** pattern = "abba", s = "dog dog dog dog"

**Output:** false 

**Constraints:**

*   `1 <= pattern.length <= 300`
*   `pattern` contains only lower-case English letters.
*   `1 <= s.length <= 3000`
*   `s` contains only lower-case English letters and spaces `' '`.
*   `s` **does not contain** any leading or trailing spaces.
*   All the words in `s` are separated by a **single space**.

## Solution

```python
from typing import Dict

class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        map: Dict[str, str] = {}
        words = s.split()
        if len(words) != len(pattern):
            return False
        for i in range(len(pattern)):
            if pattern[i] not in map:
                if words[i] in map.values():
                    return False
                map[pattern[i]] = words[i]
            else:
                if words[i] != map[pattern[i]]:
                    return False
        return True
```