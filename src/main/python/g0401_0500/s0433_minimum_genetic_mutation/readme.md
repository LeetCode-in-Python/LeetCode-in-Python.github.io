[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 433\. Minimum Genetic Mutation

Medium

A gene string can be represented by an 8-character long string, with choices from `'A'`, `'C'`, `'G'`, and `'T'`.

Suppose we need to investigate a mutation from a gene string `start` to a gene string `end` where one mutation is defined as one single character changed in the gene string.

*   For example, `"AACCGGTT" --> "AACCGGTA"` is one mutation.

There is also a gene bank `bank` that records all the valid gene mutations. A gene must be in `bank` to make it a valid gene string.

Given the two gene strings `start` and `end` and the gene bank `bank`, return _the minimum number of mutations needed to mutate from_ `start` _to_ `end`. If there is no such a mutation, return `-1`.

Note that the starting point is assumed to be valid, so it might not be included in the bank.

**Example 1:**

**Input:** start = "AACCGGTT", end = "AACCGGTA", bank = ["AACCGGTA"]

**Output:** 1 

**Example 2:**

**Input:** start = "AACCGGTT", end = "AAACGGTA", bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]

**Output:** 2 

**Example 3:**

**Input:** start = "AAAAACCC", end = "AACCCCCC", bank = ["AAAACCCC","AAACCCCC","AACCCCCC"]

**Output:** 3 

**Constraints:**

*   `start.length == 8`
*   `end.length == 8`
*   `0 <= bank.length <= 10`
*   `bank[i].length == 8`
*   `start`, `end`, and `bank[i]` consist of only the characters `['A', 'C', 'G', 'T']`.

## Solution

```python
from collections import deque
from typing import List, Set

class Solution:
    def minMutation(self, start: str, end: str, bank: List[str]) -> int:
        bank_set = set(bank)
        queue = deque([start])
        step = 0
        
        while queue:
            cur_size = len(queue)
            for _ in range(cur_size):
                cur = queue.popleft()
                if cur == end:
                    return step
                
                for next_mutation in self.getValidMutations(bank_set, cur):
                    queue.append(next_mutation)
                    bank_set.remove(next_mutation)
            step += 1
        
        return -1
    
    def getValidMutations(self, bank_set: Set[str], current: str) -> List[str]:
        valid_mutations = []
        for mutation in bank_set:
            diff = 0
            for i in range(len(mutation)):
                if mutation[i] != current[i]:
                    diff += 1
                    if diff > 1:
                        break
            if diff == 1:
                valid_mutations.append(mutation)
        return valid_mutations
```