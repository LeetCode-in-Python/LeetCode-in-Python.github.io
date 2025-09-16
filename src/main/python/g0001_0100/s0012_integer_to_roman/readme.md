[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 12\. Integer to Roman

Medium

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

    Symbol   Value
     I        1
     V        5
     X        10
     L        50
     C        100
     D        500
     M        1000

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

*   `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
*   `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
*   `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.

**Example 1:**

**Input:** num = 3

**Output:** "III" 

**Example 2:**

**Input:** num = 4

**Output:** "IV" 

**Example 3:**

**Input:** num = 9

**Output:** "IX" 

**Example 4:**

**Input:** num = 58

**Output:** "LVIII"

**Explanation:** L = 50, V = 5, III = 3. 

**Example 5:**

**Input:** num = 1994

**Output:** "MCMXCIV"

**Explanation:** M = 1000, CM = 900, XC = 90 and IV = 4. 

**Constraints:**

*   `1 <= num <= 3999`

## Solution

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        sb: list[str] = []

        def numerals(remaining: int, one: int, c_ten: str, c_five: str, c_one: str) -> int:
            div = remaining // one
            if div == 9:
                sb.append(c_one)
                sb.append(c_ten)
            elif div == 8:
                sb.append(c_five)
                sb.append(c_one)
                sb.append(c_one)
                sb.append(c_one)
            elif div == 7:
                sb.append(c_five)
                sb.append(c_one)
                sb.append(c_one)
            elif div == 6:
                sb.append(c_five)
                sb.append(c_one)
            elif div == 5:
                sb.append(c_five)
            elif div == 4:
                sb.append(c_one)
                sb.append(c_five)
            elif div == 3:
                sb.append(c_one)
                sb.append(c_one)
                sb.append(c_one)
            elif div == 2:
                sb.append(c_one)
                sb.append(c_one)
            elif div == 1:
                sb.append(c_one)
            return remaining - (div * one)

        num = numerals(num, 1000, ' ', ' ', 'M')
        num = numerals(num, 100, 'M', 'D', 'C')
        num = numerals(num, 10, 'C', 'L', 'X')
        numerals(num, 1, 'X', 'V', 'I')
        return "".join(sb)
```