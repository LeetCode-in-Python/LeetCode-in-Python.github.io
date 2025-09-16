[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 210\. Course Schedule II

Medium

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses_. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[\[1,0]]

**Output:** [0,1]

**Explanation:**

    There are a total of 2 courses to take. To take course 1 you should have finished course 0.
    So the correct course order is [0,1].

**Example 2:**

**Input:** numCourses = 4, prerequisites = \[\[1,0],[2,0],[3,1],[3,2]]

**Output:** [0,2,1,3]

**Explanation:**

    There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
    So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

**Example 3:**

**Input:** numCourses = 1, prerequisites = []

**Output:** [0] 

**Constraints:**

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= numCourses * (numCourses - 1)`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   <code>a<sub>i</sub> != b<sub>i</sub></code>
*   All the pairs <code>[a<sub>i</sub>, b<sub>i</sub>]</code> are **distinct**.

## Solution

```python
from typing import List, Dict

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = {}
        for i in range(numCourses):
            graph[i] = []
        for classes in prerequisites:
            graph[classes[0]].append(classes[1])
        output = []
        visited = {}
        for c in graph.keys():
            if self._dfs(c, graph, visited, output):
                return []
        return output

    def _dfs(self, course: int, graph: Dict[int, List[int]], 
             visited: Dict[int, bool], output: List[int]) -> bool:
        if course in visited:
            return visited[course]
        visited[course] = True
        for c in graph[course]:
            if self._dfs(c, graph, visited, output):
                return True
        visited[course] = False
        output.append(course)
        return False
```