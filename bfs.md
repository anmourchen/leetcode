# BFS (Breadth-First-Search)

## Basic Idea
* Use a **queue** to traverse the tree/graph or similar problems **in level order**
* Good for traversal or searching in a tree/graph setting
* Problems in which you have to find **shortest path** are most likely calling for a BFS
* The most difficult part is to mark the **state** you have visited

## Template

* From N-ary level order traversal

```python
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root:
            return []
        q = [root]
        // steps = 0
        res = []
        while q:
            res.append([node.val for node in q])
            level = []
            for node in q:
                for child in node.children:
                    if child:
                        level.append(child)
            q = level
            // steps += 1
        return res
```

## Related Problems
**Note**: Most problems can be solved by both BFS and DFS

### Tree
1. [102. Binary tree level order traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
2. [429. N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)
3. [863. All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)
    * Hint: Need to write a helper function to record the parent of a TreeNode using DFS
    * Hint: Need to track the distance for each level and if a TreeNode has been visited or not
4. [847. Shortest Path Visiting All Nodes](https://leetcode.com/problems/shortest-path-visiting-all-nodes/)
    * Hint: State can be represented using a tuple `(node, state)` where `state` can be represented using bits
    * Hint: Use bit operation to mark some nodes to be visited
    ```python
    for i in range(N):
            q.append((i, 1 << i))
        while q:
            level = []
            for node, state in q:
                if state == target:
                    return steps
                if visited[node][state]:
                    continue
                visited[node][state] = 1
                for nextNode in graph[node]:
                    level.append((nextNode, state | (1 << nextNode)))
            q = level
            steps += 1
        return -1
    ```
5. [117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)
   * Hint: Level order traversal and point `next` to the next element in the same level

### Graph
1. [127. Word Ladder](https://leetcode.com/problems/word-ladder/)
   * Hint: Delete a generated word from the word list after it has been visited
2. [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
   * Hint: Find the minimum cost within K distance
3. [785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
   * Hint: Use two colors to mark the visited node. If the next node has been marked as the same color, return false.
4. [752. Open the Lock](https://leetcode.com/problems/open-the-lock/)
5. [721. Account Merge](https://leetcode.com/problems/accounts-merge/)
   * Hint: For every pair of emails in the same account, draw an edge between those emails. The problem is about enumerating the connected components of this graph.
6. [815. Bus Routes *](https://leetcode.com/problems/bus-routes/)

### Chessboard or matrix
1. [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
    ```python
    for i in range(m):
        for j in range(n):
            if grid[i][j] == '1':
                counts += 1
                q = [(i, j)]
                grid[i][j] = '0'
                for x, y in q:
                    for dx, dy in dirs:
                        nx, ny = x + dx, y + dy
                        if 0 <= nx < m and 0 <= ny < n and grid[nx][ny] == '1':
                            q.append((nx, ny))
                            grid[nx][ny] = '0'
    ```
2. [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)
   * Hint: Start from four **edges** and modify the cells adjacent to `O` cells to `D`
3. [542. 01 Matrix](https://leetcode.com/problems/01-matrix/)
   * Hint: Push all the 0 cells into the queue as starting point and you can directly modify the matrix to be the distance
4. [286. Wall and Gates](https://leetcode.com/problems/walls-and-gates/)
5. [1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
6. [773. Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/)
   * Hint: Convert the board into a string and use the string as a state
7. [909. Snakes and Ladders](https://leetcode.com/problems/snakes-and-ladders/)
8. [317. Shortest Distance from All Buildings](https://leetcode.com/problems/shortest-distance-from-all-buildings/)
   * Hint: Start from each building and find the distance from the empty space to the building
   * Hint: Record the number of buildings each empty space can reach
   * Hint: Use a 2D array to record the sum of distance from each empty space to every building
