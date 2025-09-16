[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 30\. Substring with Concatenation of All Words

Hard

You are given a string `s` and an array of strings `words` of **the same length**. Return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` **exactly once**, **in any order**, and **without any intervening characters**.

You can return the answer in **any order**.

**Example 1:**

**Input:** s = "barfoothefoobarman", words = ["foo","bar"]

**Output:** [0,9]

**Explanation:** Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively. The output order does not matter, returning [9,0] is fine too. 

**Example 2:**

**Input:** s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]

**Output:** [] 

**Example 3:**

**Input:** s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]

**Output:** [6,9,12] 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of lower-case English letters.
*   `1 <= words.length <= 5000`
*   `1 <= words[i].length <= 30`
*   `words[i]` consists of lower-case English letters.

## Solution

```python
from typing import List

class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        ans = []
        n1 = len(words[0])
        n2 = len(s)
        map1 = {}
        for word in words:
            map1[word] = map1.get(word, 0) + 1
        
        for i in range(n1):
            left = i
            j = i
            c = 0
            map2 = {}
            while j + n1 <= n2:
                word1 = s[j:j + n1]
                j += n1
                if word1 in map1:
                    map2[word1] = map2.get(word1, 0) + 1
                    c += 1
                    while map2[word1] > map1[word1]:
                        word2 = s[left:left + n1]
                        map2[word2] = map2.get(word2, 0) - 1
                        left += n1
                        c -= 1
                    if c == len(words):
                        ans.append(left)
                else:
                    map2.clear()
                    c = 0
                    left = j
        
        return ans
```