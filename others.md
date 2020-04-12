# Other topics
This section covers the other algorithms or data structures that are not common, but can be useful in some problems.

## Sweep line
* Commonly used in intervals with events (with start and end)
* Usually requires sorting the events

### Related problems
* [LintCode 391. Number of Airplanes in the Sky](https://www.lintcode.com/problem/number-of-airplanes-in-the-sky)
* [218. The Skyline Problem *](https://leetcode.com/problems/the-skyline-problem/)

## Sliding window

### Basic Ideas
* Used for finding the substring/subarray that satisfies with certain conditions
* Achieved using two pointers and a hashmap. Hashmap can be used for counting the frequencies of some characters or recording the last position that a character was seen.
* Time complexity `O(n)`

### Template
```python
def findSubstring(s):
    hashmap = collections.Counter()
    counter = 0  # useful if we want to check the substring contains all the characters in another string
    left, _len = 0, 0  # left pointer and length of subtring
    for () # initialize hashmap
    for right in range(len(s)):
        hashmap[s[right]] += 1 # if hashmap is a counter
        while () {  # checking the counter conditions
        # update _len here if finding minimum length
        # increase left pointer to make substring valid/invalid again
        if hashmap[s[left]] ()  # modify the counter here
        left += 1
        }
        # update _len here if finding maximum length
    return _len
```

### Related problems
* [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
* [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
* [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
* [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
* [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
* [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
    ```python
    hashmap = {}
    left, res = 0, 0
    for right in range(len(s)):
        hashmap[s[right]] = right
        while len(hashmap.keys()) > k:
            if hashmap[s[left]] == left:
                del hashmap[s[left]]
            left += 1
        res = max(res, right - left + 1)
    return res
    ```
    * Similar problems: [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/), [992. Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/), [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/), [487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/)
* [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

## Trie

### Basic ideas
* A special kind of tree structure
* Can be defined using dictionary or simply an array of 26 elements (if `a-z`)
* Commonly used for prefix search problems

### Template
```python
class Node:
    
    def __init__(self):
        self.children = [None] * 26
        self.isword = False

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = Node()

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        current = self.root
        for c in word:
            idx = ord(c) - ord('a')
            if not current.children[idx]:
                current.children[idx] = Node()
            current = current.children[idx]
        current.isword = True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        current = self.root
        for c in word:
            idx = ord(c) - ord('a')
            if not current.children[idx]:
                return False
            current = current.children[idx]
        return current.isword

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        current = self.root
        for c in prefix:
            idx = ord(c) - ord('a')
            if not current.children[idx]:
                return False
            current = current.children[idx]
        return True
```

### Related problems
* [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefi)
* [211. Add and Search Word - Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design/)
  * Hint: Trie + DFS
* [642. Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/)
* [745. Prefix and Suffix Search](https://leetcode.com/problems/prefix-and-suffix-search/)
  * Hint: add all the possible combinations of `suffix + # + prefix` as a key for each word
* [677. Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/)

## Union Find

### Template (without ranking)
```python
class DSU:
    def __init__(self, N):
        self.parent = list(range(N))
    
    def find(self, x):
        if x != self.parent[x]:
            self.parent[x] = self.find(self.parent[x]) # 路径压缩
        return self.parent[x]
    
    def union(self, x, y):
        p, q = self.find(x), self.find(y)
        if p != q:
            self.parent[p] = q
```

### Related problems
* [305. Number of Islands II *](https://leetcode.com/problems/number-of-islands-ii/)
  * Convert the 2D matrix into a 1D array
* [947. Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)
* [1102. Path With Maximum Minimum Value](https://leetcode.com/problems/path-with-maximum-minimum-value/)
* [1135. Connecting Cities With Minimum Cost](https://leetcode.com/problems/connecting-cities-with-minimum-cost/)
* [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)
* [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)