[![](https://img.shields.io/github/stars/LeetCode-in-Python/LeetCode-in-Python?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python)
[![](https://img.shields.io/github/forks/LeetCode-in-Python/LeetCode-in-Python?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Python/LeetCode-in-Python/fork)

## 211\. Design Add and Search Words Data Structure

Medium

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

*   `WordDictionary()` Initializes the object.
*   `void addWord(word)` Adds `word` to the data structure, it can be matched later.
*   `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

**Example:**

**Input**

    ["WordDictionary","addWord","addWord","addWord","search","search","search","search"] [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
    
**Output**

    [null,null,null,null,false,true,true,true]

**Explanation**

    WordDictionary wordDictionary = new WordDictionary();
    wordDictionary.addWord("bad");
    wordDictionary.addWord("dad");
    wordDictionary.addWord("mad");
    wordDictionary.search("pad"); // return False
    wordDictionary.search("bad"); // return True
    wordDictionary.search(".ad"); // return True
    wordDictionary.search("b.."); // return True 

**Constraints:**

*   `1 <= word.length <= 500`
*   `word` in `addWord` consists lower-case English letters.
*   `word` in `search` consist of `'.'` or lower-case English letters.
*   At most `50000` calls will be made to `addWord` and `search`.

## Solution

```python
class TrieNode:
    def __init__(self):
        self.children = {}    # char -> TrieNode
        self.is_end = False   # end of word

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    # Word insert karna
    def addWord(self, word: str) -> None:
        node = self.root
        for ch in word:
            if ch not in node.children:
                node.children[ch] = TrieNode()
            node = node.children[ch]
        node.is_end = True

    # Word search karna
    def search(self, word: str) -> bool:
        def dfs(node, i):
            # Base case: agar pura word traverse ho gaya
            if i == len(word):
                return node.is_end

            ch = word[i]

            # Case 1: agar char "." hai → sab children explore karo
            if ch == ".":
                for child in node.children.values():
                    if dfs(child, i + 1):
                        return True
                return False

            # Case 2: normal character
            else:
                if ch not in node.children:
                    return False
                return dfs(node.children[ch], i + 1)

        return dfs(self.root, 0)


# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```