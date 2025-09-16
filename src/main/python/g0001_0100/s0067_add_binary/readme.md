[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 67\. Add Binary

Easy

Given two binary strings `a` and `b`, return _their sum as a binary string_.

**Example 1:**

**Input:** a = "11", b = "1"

**Output:** "100" 

**Example 2:**

**Input:** a = "1010", b = "1011"

**Output:** "10101" 

**Constraints:**

*   <code>1 <= a.length, b.length <= 10<sup>4</sup></code>
*   `a` and `b` consist only of `'0'` or `'1'` characters.
*   Each string does not contain leading zeros except for the zero itself.

## Solution

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        deci_a = int(a, 2) # Here I used the int function built-in in python and set the base to be 2 so it knows which base it is
        deci_b = int(b, 2)
        both_summed = deci_a + deci_b
        if both_summed == 0:
            return "0"
        binary_form = []
        while both_summed > 0:
            remainder = both_summed % 2
            binary_form.insert(0, str(remainder)) # Here I used insert so I could insert at first index so i wouldnt have to reverse it
            both_summed //= 2

        return "".join(binary_form) # Here I had to use join i could use print beacause leetcodes expects returned value so I use "" as seperator and joined the variable
```