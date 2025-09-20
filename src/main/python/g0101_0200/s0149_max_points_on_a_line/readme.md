[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 149\. Max Points on a Line

Hard

Given an array of `points` where <code>points[i] = [x<sub>i</sub>, y<sub>i</sub>]</code> represents a point on the **X-Y** plane, return _the maximum number of points that lie on the same straight line_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane1.jpg)

**Input:** points = \[\[1,1],[2,2],[3,3]]

**Output:** 3 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane2.jpg)

**Input:** points = \[\[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]

**Output:** 4 

**Constraints:**

*   `1 <= points.length <= 300`
*   `points[i].length == 2`
*   <code>-10<sup>4</sup> <= x<sub>i</sub>, y<sub>i</sub> <= 10<sup>4</sup></code>
*   All the `points` are **unique**.

## Solution

```python
from typing import List

class Solution:
    def maxPoints(self, points: List[List[int]]) -> int:
        result = min(len(points), 2)
        n = len(points)
        for i in range(n):
            hashmap = {}
            for j in range(n):
                x1, y1 = points[i]
                x2, y2 = points[j]
                if x2 - x1 == 0:
                    m = float("inf")
                else:
                    m = (y2 - y1) / (x2 - x1)
                if m in hashmap:
                    hashmap[m].add(i)
                    hashmap[m].add(j)
                else:
                    hashmap[m] = set([i, j])                
                result = max(len(hashmap[m]), result)
        
        return result
```