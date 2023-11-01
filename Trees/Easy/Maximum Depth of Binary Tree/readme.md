# Maximum Depth of Binary Tree

## Problem Link

https://leetcode.com/problems/maximum-depth-of-binary-tree/

## Solutions

### Solution 1: Recursive DFS Approach

#### Implementation

The method uses recursion to traverse the binary tree and calculate the maximum depth. The function just checks if the root exists, if it exists it return max of left and right subtree plus one, if not it returns a 0.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root: return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(h), where h is the height of the tree

### Solution 2: Iterative DFS Approach

#### Implementation

This aproach uses a Stack to iteratively traverse a tree. The stack stores pair of node and depth of that node. For each iteration, the stack is popped to get a node and its depth, if the node exists we update the max depth.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        
        h = 0
        stack = [[root, 1]]

        while stack:
            cur, depth = stack.pop()

            if cur:
                h = max(h, depth)
                stack.append([cur.left,depth+1])
                stack.append([cur.right,depth+1])

        return h
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 3: Iterative BFS Approach

#### Implementation

This aproach uses a Queue to iteratively traverse a tree. The tree is traversed in level Order. The levels are counted and the count is returned.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        
        h = 0
        q = deque()
        if root:
            q.append(root)
        
        while q:
            h += 1
            for i in range(len(q)):
                cur = q.popleft()
                if cur.left: q.append(cur.left)
                if cur.right: q.append(cur.right)

        return h
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(2^(h-1))

