[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 416\. Partition Equal Subset Sum

Medium

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

**Input:** nums = [1,5,11,5]

**Output:** true

**Explanation:** The array can be partitioned as [1, 5, 5] and [11]. 

**Example 2:**

**Input:** nums = [1,2,3,5]

**Output:** false

**Explanation:** The array cannot be partitioned into equal sum subsets. 

**Constraints:**

*   `1 <= nums.length <= 200`
*   `1 <= nums[i] <= 100`

## Solution

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sums = sum(nums)
        if sums % 2 == 1:
            return False
        sums //= 2
        dp = [False] * (sums + 1)
        dp[0] = True
        for num in nums:
            for i in range(sums, num - 1, -1):
                dp[i] = dp[i] or dp[i - num]
        return dp[sums]
```