# DFS (Depth-First-Search)

## Basic idea

* Use recursion to solve the problem, sometimes can go very deep
* Good for traversal or searching in a tree/graph setting
* Similar to BFS, we need to track if the state has been visited before or not to avoid infinite loop

## Template (without backtracking)

From Number of Islands  
**Note**: We do not need to track if each cell has been visited or not as we can just modify the visited cell to be 0

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0
        m, n = len(grid), len(grid[0])
        nums = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    self.dfs(grid, i, j)
                    nums += 1
        return nums
    
    def dfs(self, grid, x, y):
        m, n = len(grid), len(grid[0])
        dirs = [[-1, 0], [1, 0], [0, -1], [0, 1]]
        # visited[x][y] = True
        grid[x][y] = '0'
        for dx, dy in dirs:
            nx, ny = x + dx, y + dy
            if 0 <= nx < m and 0 <= ny < n and grid[nx][ny] == '1':
            # if 0 <= nx < m and 0 <= ny < n and not visited[nx][ny]:
                self.dfs(grid, nx, ny)
```

## Related Problems

### Chessboard or matrix problems

1. [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
    * Need to know how to solve using both BFS and DFS
2. [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
3. [329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)
    * Need to use a 2D array to cache the results to avoid repeated computations.
    * When you visit four adjacent cells, you need to record the maximum length of path in four directions.
4. [1066. Campus Bikes II](https://leetcode.com/problems/campus-bikes-ii/)
    * Hint: Need memorization
5. [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)
    * Need two boolean arrays to track if the current position can reach Pacific and Atlantic, respectively
    * Start from four borders and move to the next position with larger height
6. [694. Number of Distinct Islands](https://leetcode.com/problems/number-of-distinct-islands/)
    * Extension to LC 200, subtract each point by the coordinates for top left point

### Graph problems

1. [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)
    * Very similar to LC 547, this is the generalization of friend circles in the graph setting.
2. [547. Friend Circles](https://leetcode.com/problems/friend-circles/)
3. [399. Evaluate Division](https://leetcode.com/problems/evaluate-division/)
4. [841. Keys and Rooms](https://leetcode.com/problems/keys-and-rooms/)
    * Determine if a graph is a connected component
5. [261. Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)
    * A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.
6. [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
   * Hint: Use a hashmap
7. [332. Reconstruct Itinerary *](https://leetcode.com/problems/reconstruct-itinerary/)
    * Sort the children in the graph
    * Post-order traversal and reverse the final result
8. [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)
    * Can be solved using DFS (`O(n^2)`, not optimal)
    * Iterate over each edge and check if there is already a path between these two nodes, if `True`, return this edge.
9. [1192. Critical Connections in a Network *](https://leetcode.com/problems/critical-connections-in-a-network/)
   * depth: the "depth" of each node in the DFS tree. It's the "sequence number" of nodes we visit rather than the actual depth, keep that in mind.
   * lowest: the lowest (in terms of sequence number/depth) node we can visit though the subtree of the node. This is the key part: if we can visit lower (close to the top) nodes through (parent, child) than parent itself, it means child is accessible in at least two routes, and hence (u,v) is not a cricital edge (and vise versa).
10. [465. Optimal Account Balancing *](https://leetcode.com/problems/optimal-account-balancing/)
    * Hint: DFS + memorization
    * Hint: state is the current `assets` and `debts`. Sort them reversely so we want to balanace the highest debts first

### Topological sorting

1. [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
    * BFS  
    Find the node that has a zero indegree, delete that node from the graph. If cannot find such a node, return `False`.
    ```python
    for u, v in prerequisites:
        graph[v].append(u)
        indegree[u] += 1
    for i in range(numCourses):
        zeroDegree = False
        for j in range(numCourses):
            if indegree[j] == 0:
                zeroDegree = True
                break
        if not zeroDegree:
            return False
        indegree[j] -= 1
        for node in graph[j]:
            indegree[node] -= 1
    return True
    ```
    * DFS  
    `visited[i] == 0` means unvisited, `1` means visiting and `2` means visited. If we visit a node has been marked as visiting, then return `False`.
    ```python
    visited = [0 for i in range(numCourses)]
    for i in range(numCourses):
        if not self.dfs(graph, i, visited):
            return False
    return True
    
    def dfs(self, graph, i, visited):
        if visited[i] == 2:  # return True if the current node has been visited
            return True
        if visited[i] == 1: # has been marked visiting
            return False
        visited[i] = 1  # mark visiting
        for j in graph[i]:
            if not self.dfs(graph, j, visited):
                return False
        visited[i] = 2  # mark visited
        return True
    ```
2. [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

3. [269. Alien Dictionary *](https://leetcode.com/problems/alien-dictionary/)
    * Hint: first construct the graph, then do topological sorting

### Tree problems
**Note**: Tree traversal: pre-order, in-order and post-oder  
**Note**: In-order transversal of a BST is a sorted array

1. [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
2. [112. Path Sum](https://leetcode.com/problems/path-sum/)
3. [437. Path Sum iii](https://leetcode.com/problems/path-sum-iii/)
4. [124. Binary Tree Maximum Path Sum *](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
   * Hint: only root and one child can be used for local maximum
   * Hint: root and both children can be used for global maximum (Cannot pass this result to the root)
   * Similar problem: [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
5. [366. Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/)
6. [337. House Robber III](https://leetcode.com/problems/house-robber-iii/)
   * Hint: Find the maximum between `root.val + grandchildren.val` and `root.left.val + root.right.val`
7. [889. Construct Binary Tree from Preorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/), [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/), [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/).
   * Hint: determine the location of the root and then solve recursively
8. [834. Sum of Distances in Tree *](https://leetcode.com/problems/sum-of-distances-in-tree/)
    * Hint: `res[x] = res[y] - #(X) + N - #(X)` 
9. [1110. Delete Nodes And Return Forest](https://leetcode.com/problems/delete-nodes-and-return-forest/), [814. Binary Tree Pruning](https://leetcode.com/problems/binary-tree-pruning/)

### General problems

1. [301. Remove Invalid Parentheses *](https://leetcode.com/problems/remove-invalid-parentheses/)
   * Hint: Check if a string is valid in parentheses
   * Compute the number of misplaced `(` and `)`
   * Use DFS to remove the misplaced parentheses, remove `)` first and then `(`
   ```python
   class Solution:
        def removeInvalidParentheses(self, s: str) -> List[str]:
            l, r = 0, 0
            res = []
            for c in s:
                l += (c == '(')
                if l == 0:
                    r += (c == ')')
                else:
                    l -= (c == ')')
            self.dfs(s, 0, l, r, res)
            return res
    
        def dfs(self, s, start, l, r, res):
            if l == 0 and r == 0 and self.isValid(s):
                res.append(s)
                return
            for i in range(start, len(s)):
                if i > start and s[i] == s[i - 1]:
                    continue
                if s[i] == '(' or s[i] == ')':
                    if l > 0 and s[i] == '(':
                        self.dfs(s[: i] + s[i + 1: ], i, l - 1, r, res)
                    if r > 0 and s[i] == ')':
                        self.dfs(s[: i] + s[i + 1: ], i, l, r - 1, res)
                
        def isValid(self, s):
            count = 0
            for c in s:
                if c == '(':
                    count += 1
                elif c == ')':
                    count -= 1
                if count < 0:
                    return False
            return True
   ```
2. [472. Concatenated Words](https://leetcode.com/problems/concatenated-words/)
   * Hint: Can also solve using dynamic programming
3. [211. Add and Search Word - Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design/)
   * Hint: Trie + DFS
4. Parsing the strings
   * Usually can be solved using stacks 
   * [394. Decode String](https://leetcode.com/problems/decode-string/)
   * [1096. Brace Expansion II*](https://leetcode.com/problems/brace-expansion-ii/)
   * [772. Basic Calculator III*](https://leetcode.com/problems/basic-calculator-iii/)
   * [726. Number of Atoms](https://leetcode.com/problems/number-of-atoms/)

### BFS + DFS problems
1. [126. Word Ladder II *](https://leetcode.com/problems/word-ladder-ii/)
    * Hint: BFS to construct the graphm. Use a dictionary to record the parent word of the current transformed word
    * Hint: DFS to find the path
```python
# BFS part
while q and not found:
    for word in q:
        visited.add(word) # need to mark visited here becasue nextWord might be duplicated and we want to allow it
    nextSet = set()
    for word in q:
        for i in range(len(word)):
            for j in string.ascii_lowercase:
                if j == word[i]:
                    continue
                nextWord = word[: i] + j + word[i + 1: ]
                if nextWord not in visited and nextWord in wordList:
                    if nextWord == endWord:
                        found = True # Do not break
                    nextSet.add(nextWord)
                    graph[nextWord].append(word) # record parent node
    q = nextSet

# DFS part
def dfs(self, graph, res, path, word):
    if not graph[word]:
        res.append([word] + path) # becasue we start from endWord
    for parent in graph[word]:
        self.dfs(graph, res, [word] + path, parent)
```
2. [934. Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)
    * Find an island and use DFS to mark all the island to be `2`. Also push this island to a queue
   * Use BFS to find the shortest distance from this marked island to other island (which is all `1` s)
