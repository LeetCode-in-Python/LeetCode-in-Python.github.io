121\. Best Time to Buy and Sell Stock

Easy

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

**Input:** prices = [7,1,5,3,6,4]

**Output:** 5

**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5. Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell. 

**Example 2:**

**Input:** prices = [7,6,4,3,1]

**Output:** 0

**Explanation:** In this case, no transactions are done and the max profit = 0. 

**Constraints:**

*   <code>1 <= prices.length <= 10<sup>5</sup></code>
*   <code>0 <= prices[i] <= 10<sup>4</sup></code>

To solve this task, we can use a greedy approach. We'll iterate through the prices array and keep track of the minimum price seen so far and the maximum profit we can achieve. Here are the steps:

1. Define the `Solution` class.
2. Define the `maxProfit` method which takes `prices` as input.
3. Initialize variables `min_price` to store the minimum price seen so far and `max_profit` to store the maximum profit.
4. Iterate through the `prices` array.
5. Update `min_price` to the minimum of the current price and `min_price`.
6. Update `max_profit` to the maximum of the difference between the current price and `min_price`, and `max_profit`.
7. After iterating through the array, return `max_profit`.

Here's the Python code implementing these steps:

```python
class Solution:
    def maxProfit(self, prices):
        if not prices or len(prices) == 1:
            return 0
        
        min_price = prices[0]
        max_profit = 0
        
        for price in prices[1:]:
            min_price = min(min_price, price)
            max_profit = max(max_profit, price - min_price)
        
        return max_profit
```

You can then use this `Solution` class to find the maximum profit you can achieve by buying and selling stocks.