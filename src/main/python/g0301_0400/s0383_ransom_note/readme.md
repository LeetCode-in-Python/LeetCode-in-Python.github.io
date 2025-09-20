[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 383\. Ransom Note

Easy

Given two stings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**

**Input:** ransomNote = "a", magazine = "b"

**Output:** false

**Example 2:**

**Input:** ransomNote = "aa", magazine = "ab"

**Output:** false

**Example 3:**

**Input:** ransomNote = "aa", magazine = "aab"

**Output:** true

**Constraints:**

*   <code>1 <= ransomNote.length, magazine.length <= 10<sup>5</sup></code>
*   `ransomNote` and `magazine` consist of lowercase English letters.

## Solution

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        freq = [0] * 26
        n = len(ransomNote)
        for i in range(n):
            freq[ord(ransomNote[i]) - 97] += 1
        for i in range(len(magazine)):
            if n == 0:
                break
            if freq[ord(magazine[i]) - 97] > 0:
                n -= 1
                freq[ord(magazine[i]) - 97] -= 1
        return n == 0
```