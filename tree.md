# Tree

## Basic ideas

* Tree is defined in a recursive fashion, thus tree problems are commonly solved using recursion, BFS or DFS
* Tree traversal: pre-order, in-order and post-order
* Binary Search Tree is a special kind of tree where **in-order traversal** is a sorted array

## Template
* Iterative traversal 
    * Pre-order
    ```python
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        res, stack = [], [root]
        while stack:
            node = stack.pop()
            if not node:
                continue
            res.append(node.val)
            stack.append(node.right)  # append right child first as we are poping the last element first
            stack.append(node.left)
        return res
    ```
    * In-order
    ```python
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res, stack = [], []
        while True:
            while root:
                stack.append(root)
                root = root.left
            if not stack:
                return res
            root = stack.pop()
            res.append(root.val)
            root = root.right
        return res
    ```
    * Post-order
    ```python
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        res, stack = [], [root]
        while stack:
            node = stack.pop()
            if not node:
                continue
            res.append(node.val)
            stack.append(node.left)
            stack.append(node.right)
        return res[:: -1]
    ```

## Related problems

### Tree traversal
1. [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/), [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/), [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
   * Hint: Iterative solution using stack
2. [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
    ```python
    def toTree(self, data):  # deserialize tree
        if data[0] == 'null':
            data.pop(0)
            return None
        root = TreeNode(int(data[0]))
        data.pop(0)  # pop the first element after traversal
        root.left = self.toTree(data)
        root.right = self.toTree(data)
        return root
    ```
    * Similar problems: [449. Serialize and Deserialize BST](https://leetcode.com/problems/serialize-and-deserialize-bst/) (optimize the space using post-order traversal), [428. Serialize and Deserialize N-ary Tree *](https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/) (Append the number of children in serialization), [652. Find Duplicate Subtrees](https://leetcode.com/problems/find-duplicate-subtrees/) (Use serialization to represent the subtree structure and hashmap)
3. [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)
   * Pre-order traversal and store the nodes in a list
4. [1026. Maximum Difference Between Node and Ancestor](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/)
   * Hint: *Pre-order* traversal will preserve the relationship between the ancestor and its descendents. Also need to use *local* min and max value to record the maximum difference.

### BST
**Note:** In-order traversal of BST is a sorted array.
1. [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)
   * Hint: Use stack to in-order tranverse the BST
2. [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
   * Hint: Use stack for in-order traversal
3. [272. Closest Binary Search Tree Value II *](https://leetcode.com/problems/closest-binary-search-tree-value-ii/)
   * Hint: Use two stacks
4. [285. Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/), [510. Inorder Successor in BST II](https://leetcode.com/problems/inorder-successor-in-bst-ii/)
5. [255. Verify Preorder Sequence in Binary Search Tree](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/)
6. [333. Largest BST Subtree](https://leetcode.com/problems/largest-bst-subtree/)
7. [538. Convert BST to Greater Tree](https://leetcode.com/problems/convert-bst-to-greater-tree/)
8. [99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)
   * Hint: Use three pointers and in-order traversal `[1, 5*, 2, 3, 4, 2*]  - > [1, 2, 3, 4, 5]`
9.  [95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

### Recursion
1. [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
2. [987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)
3. [572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
   * Hint: Use a helper function to determine if two trees are the same
4. [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)
   * Hint: Compute the height of left and right trees to determine which subtree is a full binary tree
5. [250. Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees/)
6. [958. Check Completeness of a Binary Tree](https://leetcode.com/problems/check-completeness-of-a-binary-tree/)
   * Hint: BFS