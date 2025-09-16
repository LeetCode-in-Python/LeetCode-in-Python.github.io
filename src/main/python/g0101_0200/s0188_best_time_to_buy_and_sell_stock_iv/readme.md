[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 188\. Best Time to Buy and Sell Stock IV

Hard

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the <code>i<sup>th</sup></code> day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**

**Input:** k = 2, prices = [2,4,1]

**Output:** 2

**Explanation:** Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2. 

**Example 2:**

**Input:** k = 2, prices = [3,2,6,5,0,3]

**Output:** 7

**Explanation:** Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3. 

**Constraints:**

*   `0 <= k <= 100`
*   `0 <= prices.length <= 1000`
*   `0 <= prices[i] <= 1000`

## Solution

```python
from typing import List

class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        n = len(prices)
        dp = [0] * (k + 1)
        maxdp = [float('-inf')] * (k + 1)
        
        for i in range(1, n + 1):
            maxdp[0] = max(maxdp[0], dp[0] - prices[i - 1])
            for j in range(k, 0, -1):
                maxdp[j] = max(maxdp[j], dp[j] - prices[i - 1])
                dp[j] = max(maxdp[j - 1] + prices[i - 1], dp[j])
        
        return dp[k]
```