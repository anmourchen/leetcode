# Backtracking

## Basic idea

* Special case of DFS
* Try to use the current state to find the solution. If it does not work, reset the current state.

## Template
```python
    def dfs(nums, index, visited, res, path):
        if index == len(nums):
            res.append(path)
            return
        for i in range(index, len(nums)):
            if not visited[i]:
                visited[i] = True
                path.append(nums[i])
                self.dfs(nums, index + 1, visited, res, path)  # try nums[i]
                path.pop()  # backtracking
                visited[i] = False

```

## Related problems

### Finding all combinations
1. [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)  
    **Same problems** (can be solved by purely DFS or backtracking)
    * [46. Permutations](https://leetcode.com/problems/permutations/), [47. Permutations II](https://leetcode.com/problems/permutations-ii/)
    * [77. Combinations](https://leetcode.com/problems/combinations/)
    * [39. Combination Sum](https://leetcode.com/problems/combination-sum/), [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/), [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
    * [78. Subsets](https://leetcode.com/problems/subsets/), [90. Subsets II](https://leetcode.com/problems/subsets-ii/)
2. [254. Factor Combinations](https://leetcode.com/problems/factor-combinations/)
3. [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)
4. [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
   * Hint: use `left` and `right` to record the remaining number of left and right parentheses. It must satisfy `left >= right`
5. [698. Partition to K Equal Sum Subsets](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)
   * Hint: set target as K equal sums and use DFS with backtracking to try to skip the current number
    ```python
    def dfs(self, nums, i, k, target):
        if i == len(nums):
            return True
        num = nums[i]
        for j in range(k):
            if target[j] >= num:
                target[j] -= num
                if self.dfs(nums, i + 1, k, target):
                    return True
                target[j] += num
        return False
    ```
    * Same problems: [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) and [473. Matchsticks to Square](https://leetcode.com/problems/matchsticks-to-square/)
6. [93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/)
   * Hint: Check `if len(s) > (4 - len(path)) * 3` in DFS to reduce the computation time
7. [140. Word Break II *](https://leetcode.com/problems/word-break-ii/)
8. [291. Word Pattern II *](https://leetcode.com/problems/word-pattern-ii/)

### Chessboard or matrix
1. [79. Word Search](https://leetcode.com/problems/word-search/)
    ```python
    def dfs(self, board, x, y, n, word):
        if n == len(word):
            return True
        dirs = [[-1, 0], [1, 0], [0, -1], [0, 1]]
        board[x][y] = board[x][y].swapcase()  # mark as visited
        for dx, dy in dirs:
            nx, ny = x + dx, y + dy
            if 0 <= nx < len(board) and 0 <= ny < len(board[0]) and board[nx][ny] == word[n]:
                if self.dfs(board, nx, ny, n + 1, word):
                    return True
        board[x][y] = board[x][y].swapcase()  # backtrack
        return False
    ```
    * Follow up: [212. Word Search II *](https://leetcode.com/problems/word-search-ii/) (DFS + Trie)
    ```python
    for i in range(m):
            for j in range(n):
                idx = ord(board[i][j]) - ord('a')
                if root.children[idx]:
                    self.dfs(board, i, j, board[i][j], root.children[idx], res)
        return list(res)
    
    def dfs(self, board, x, y, path, root, res):
        if root.isword:
            res.add(path)  # do not return
        board[x][y] = board[x][y].swapcase()
        dirs = [[-1, 0], [1, 0], [0, -1], [0, 1]]
        for dx, dy in dirs:
            nx, ny = x + dx, y + dy
            if 0 <= nx < len(board) and 0 <= ny < len(board[0]):
                idx = ord(board[nx][ny]) - ord('a')
                if idx >= 0 and root.children[idx]:
                    self.dfs(board, nx, ny, path + board[nx][ny], root.children[idx], res)
        board[x][y] = board[x][y].swapcase()
    ```
2. [52. N-Queens II *](https://leetcode.com/problems/n-queens-ii/)
   * Follow up: [51. N-Queens](https://leetcode.com/problems/n-queens/)
   * Hint: Use a 1D array `board[row]` to record the column number where a queen has been put in row number `row`
3. [37. Sudoku Solver *](https://leetcode.com/problems/sudoku-solver/)
   * Hint: solve the sudoku from left to right, top to bottom
4. [980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii/)
   * Hint: track the number of `0` cells have visited