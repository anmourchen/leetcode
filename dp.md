# Dynamic Programming (DP)

## Basic idea
* Used to solve the problems that BFS or DFS will TLE
* The most difficult part is the transfer function, i.e., how to relate the current state to the previous state

## Template


## Related problems

### 1D Array
1. [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
   * Similar problem: [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
2. [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
   * Similar problems: [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/), [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/), [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/), [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
3. [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
   * Similar problems: [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/), [198. House Robber](https://leetcode.com/problems/house-robber/), [213. House Robber II](https://leetcode.com/problems/house-robber-ii/), [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/), [801. Minimum Swaps To Make Sequences Increasing](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/), [926. Flip String to Monotone Increasing](https://leetcode.com/problems/flip-string-to-monotone-increasing/), [256. Paint House](https://leetcode.com/problems/paint-house/), [265. Paint House II *](https://leetcode.com/problems/paint-house-ii/)
4. [139. Word Break](https://leetcode.com/problems/word-break/)
   * `dp[i]` to represent if string `s[0: i]` can be segmented into a sequence of dictionary words
5. [97. Interleaving String](https://leetcode.com/problems/interleaving-string/)
   * `dp[i][j]` to represent whether `s3[0:i+j]` can be formed by interleaving `s1[0:i]` and `s2[0:j]`
6. [1048. Longest String Chain](https://leetcode.com/problems/longest-string-chain/)
   * For each word in order of length, for each word2 which is word with one character removed, `length[word2] = max(length[word2], length[word] + 1)`
7. [91. Decode Ways](https://leetcode.com/problems/decode-ways/)
8. [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/), [1027. Longest Arithmetic Sequence](https://leetcode.com/problems/longest-arithmetic-sequence/), [1218. Longest Arithmetic Subsequence of Given Difference](https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/)
9. [516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/), [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/), [115. Distinct Subsequences *](https://leetcode.com/problems/distinct-subsequences/)
    * `dp[i][j]` = longest palindromic subsequence length for substring `s[i: j + 1]`
10. [72. Edit Distance *](https://leetcode.com/problems/edit-distance/)
   * `dp[i][j]` to represent the minimum number of operations to convert `word1[: i]` to `word2[: j`
11. [10. Regular Expression Matching *](https://leetcode.com/problems/regular-expression-matching/)
    ```python
    def isMatch(self, s: str, p: str) -> bool:
        dp = [[False for j in range(len(p) + 1)] for i in range(len(s) + 1)]
        dp[0][0] = True
        for j in range(1, len(p)):
            if p[j] == '*':
                dp[0][j + 1] = dp[0][j - 1]
        for i in range(len(s)):
            for j in range(len(p)):
                if s[i] == p[j] or p[j] == '.':
                    dp[i + 1][j + 1] = dp[i][j]
                elif p[j] == '*':
                    if s[i] != p[j - 1] and p[j - 1] != '.':
                        dp[i + 1][j + 1] = dp[i + 1][j - 1]
                    else:
                        dp[i + 1][j + 1] = dp[i + 1][j] or dp[i][j + 1] or dp[i + 1][j - 1]
        return dp[len(s)][len(p)]
    ```
    * Similar problem: [44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)
12. [322. Coin Change](https://leetcode.com/problems/coin-change/)
   * `dp[i]` is the minimum count for amounts up to `i`
13. [935. Knight Dialer](https://leetcode.com/problems/knight-dialer/)
14. [312. Burst Balloons *](https://leetcode.com/problems/burst-balloons/)
    * `dp[i][j]` = max coins (`nums[i: j + 1]`
    * Can also solve using DFS
15. [1130. Minimum Cost Tree From Leaf Values](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/)
    * `dp[i][j]` is the minimum cost for the subarray `arr[i]..arr[j]`.

### 2D matrix

1. [221. Maximal Square](https://leetcode.com/problems/maximal-square/)
   * `dp[i][j]` is the length of the square from `(0, 0)` to `(i, j)`
2. [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)
3. [741. Cherry Pickup *](https://leetcode.com/problems/cherry-pickup/)
   * DFS with memorization, can think of two persons starting from `(n - 1, n - 1)` to `(0, 0)` at the same time
4. [688. Knight Probability in Chessboard](https://leetcode.com/problems/knight-probability-in-chessboard/)
