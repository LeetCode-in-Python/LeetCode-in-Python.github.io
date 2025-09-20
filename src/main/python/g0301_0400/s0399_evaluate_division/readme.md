[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 399\. Evaluate Division

Medium

You are given an array of variable pairs `equations` and an array of real numbers `values`, where <code>equations[i] = [A<sub>i</sub>, B<sub>i</sub>]</code> and `values[i]` represent the equation <code>A<sub>i</sub> / B<sub>i</sub> = values[i]</code>. Each <code>A<sub>i</sub></code> or <code>B<sub>i</sub></code> is a string that represents a single variable.

You are also given some `queries`, where <code>queries[j] = [C<sub>j</sub>, D<sub>j</sub>]</code> represents the <code>j<sup>th</sup></code> query where you must find the answer for <code>C<sub>j</sub> / D<sub>j</sub> = ?</code>.

Return _the answers to all queries_. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Example 1:**

**Input:** equations = \[\["a","b"],["b","c"]], values = [2.0,3.0], queries = \[\["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]

**Output:** [6.00000,0.50000,-1.00000,1.00000,-1.00000]

**Explanation:**

Given: _a / b = 2.0_, _b / c = 3.0_

queries are: _a / c = ?_, _b / a = ?_, _a / e = ?_, _a / a = ?_, _x / x = ?_

return: [6.0, 0.5, -1.0, 1.0, -1.0 ]

**Example 2:**

**Input:** equations = \[\["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = \[\["a","c"],["c","b"],["bc","cd"],["cd","bc"]]

**Output:** [3.75000,0.40000,5.00000,0.20000]

**Example 3:**

**Input:** equations = \[\["a","b"]], values = [0.5], queries = \[\["a","b"],["b","a"],["a","c"],["x","y"]]

**Output:** [0.50000,2.00000,-1.00000,-1.00000]

**Constraints:**

*   `1 <= equations.length <= 20`
*   `equations[i].length == 2`
*   <code>1 <= A<sub>i</sub>.length, B<sub>i</sub>.length <= 5</code>
*   `values.length == equations.length`
*   `0.0 < values[i] <= 20.0`
*   `1 <= queries.length <= 20`
*   `queries[i].length == 2`
*   <code>1 <= C<sub>j</sub>.length, D<sub>j</sub>.length <= 5</code>
*   <code>A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub></code> consist of lower case English letters and digits.

## Solution

```python
from typing import Dict, List

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        self.root: Dict[str, str] = {}
        self.rate: Dict[str, float] = {}
        
        # Initialize all variables
        for equation in equations:
            x, y = equation[0], equation[1]
            self.root[x] = x
            self.root[y] = y
            self.rate[x] = 1.0
            self.rate[y] = 1.0
        
        # Union all equations
        for i, equation in enumerate(equations):
            x, y = equation[0], equation[1]
            self.union(x, y, values[i])
        
        # Process queries
        result = []
        for query in queries:
            x, y = query[0], query[1]
            if x not in self.root or y not in self.root:
                result.append(-1.0)
                continue
            
            root_x = self.findRoot(x, x, 1.0)
            root_y = self.findRoot(y, y, 1.0)
            
            if root_x == root_y:
                result.append(self.rate[x] / self.rate[y])
            else:
                result.append(-1.0)
        
        return result
    
    def union(self, x: str, y: str, v: float) -> None:
        root_x = self.findRoot(x, x, 1.0)
        root_y = self.findRoot(y, y, 1.0)
        self.root[root_x] = root_y
        r1 = self.rate[x]
        r2 = self.rate[y]
        self.rate[root_x] = v * r2 / r1
    
    def findRoot(self, original_x: str, x: str, r: float) -> str:
        if self.root[x] == x:
            self.root[original_x] = x
            self.rate[original_x] = r * self.rate[x]
            return x
        return self.findRoot(original_x, self.root[x], r * self.rate[x])
```