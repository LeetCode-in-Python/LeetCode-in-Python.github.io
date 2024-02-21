128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4. 

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9 

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

To solve this task efficiently in O(n) time, we can use a HashSet to store all the elements of the array. Then, we can iterate through the array and for each element, check if the previous consecutive element (element - 1) exists in the set. If it does not exist, it means that the current element is the start of a new consecutive sequence. We can then keep track of the length of the consecutive sequence starting from the current element by continuously incrementing the current element until it no longer exists in the set. At each step, we update the maximum length of consecutive elements encountered so far. Here are the steps:

1. Define the `Solution` class.
2. Define the `longestConsecutive` method which takes `nums` as input.
3. Create a set `num_set` to store all elements of the array.
4. Initialize a variable `max_length` to store the maximum length of consecutive sequence encountered so far.
5. Iterate through the elements of the array.
6. For each element `num`, check if `num - 1` exists in `num_set`. If it does not exist, it means that `num` is the start of a new consecutive sequence.
7. Increment `current_length` by 1 and continuously increment `num` until it no longer exists in `num_set`.
8. Update `max_length` with the maximum of `max_length` and `current_length`.
9. After iterating through all elements, return `max_length`.

Here's the Python code implementing these steps:

```python
class Solution:
    def longestConsecutive(self, nums):
        num_set = set(nums)
        max_length = 0
        
        for num in nums:
            if num - 1 not in num_set:
                current_num = num
                current_length = 1
                
                while current_num + 1 in num_set:
                    current_num += 1
                    current_length += 1
                
                max_length = max(max_length, current_length)
        
        return max_length
```

You can then use this `Solution` class to find the length of the longest consecutive elements sequence in the given unsorted array.