[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 68\. Text Justification

Hard

Given an array of strings `words` and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified and no extra space is inserted between words.

**Note:**

*   A word is defined as a character sequence consisting of non-space characters only.
*   Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
*   The input array `words` contains at least one word.

**Example 1:**

**Input:** words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16

**Output:** [ "This is an", "example of text", "justification. " ]

**Example 2:**

**Input:** words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16

**Output:** [ "What must be", "acknowledgment ", "shall be " ]

**Explanation:** Note that the last line is "shall be " instead of "shall be", because the last line must be left-justified instead of fully-justified. Note that the second line is also left-justified becase it contains only one word.

**Example 3:**

**Input:** words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20

**Output:** [ "Science is what we", "understand well", "enough to explain to", "a computer. Art is", "everything else we", "do " ]

**Constraints:**

*   `1 <= words.length <= 300`
*   `1 <= words[i].length <= 20`
*   `words[i]` consists of only English letters and symbols.
*   `1 <= maxWidth <= 100`
*   `words[i].length <= maxWidth`

## Solution

```python
from typing import List

class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        # Trying to gauge the number of lines so the list doesn't need to resize
        output = []
        # Setting string capacity also
        sb = []
        line_total = 0
        num_words_on_line = 0
        start_word = 0
        # looping until the 2nd last word, since we're checking words[i + 1] for overflows
        for i in range(len(words) - 1):
            line_total += len(words[i])
            # tracking line length + #words
            num_words_on_line += 1
            # checking if the next word causes an overflow
            if line_total + num_words_on_line + len(words[i + 1]) > maxWidth:
                # if only one word fits on the line...
                if num_words_on_line == 1:
                    # append word
                    sb.append(words[i])
                    # pad right with spaces
                    while line_total < maxWidth:
                        sb.append(' ')
                        line_total += 1
                else:
                    # # of extra spaces
                    extra_sp = (maxWidth - line_total) % (num_words_on_line - 1)
                    # Creating the line
                    for j in range(start_word, start_word + num_words_on_line - 1):
                        # appending the word
                        sb.append(words[j])
                        if extra_sp > 0:
                            # appending an extra space, if required
                            sb.append(' ')
                            extra_sp -= 1
                        # appending the rest of the required spaces
                        max_spaces = max(0, (maxWidth - line_total) # (num_words_on_line - 1))
                        sb.append(' ' * max_spaces)
                    # appending the last word of the line
                    sb.append(words[start_word + num_words_on_line - 1])
                # adding to output list
                output.append(''.join(sb))
                # reset everything for next line
                # keeping track of the first word for next line
                start_word = i + 1
                # resetting these to 0 for processing next line
                num_words_on_line = line_total = 0
                # need a new list for the next line
                sb = []
        # handling the final line (no justification, right padded with spaces)
        line_total = 0
        for i in range(start_word, len(words)):
            line_total += len(words[i])
            sb.append(words[i])
            if line_total < maxWidth:
                sb.append(' ')
                line_total += 1
        # padding right side with spaces
        while line_total < maxWidth:
            sb.append(' ')
            line_total += 1
        # add the final line to output list
        output.append(''.join(sb))
        return output
```