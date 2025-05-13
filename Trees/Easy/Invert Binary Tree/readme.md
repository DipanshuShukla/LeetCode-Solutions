# Invert Binary Tree

## Problem Link

https://leetcode.com/problems/invert-binary-tree/

## Solutions

### Solution 1: Using a queue [Level order Traversal]

#### Implementation

The method uses an iterative approach and uses a queue to traverse a tree. We start to traverse a queue containing the root node in the begining. During each iteration, we swap the left and right node of the current node popped from the queue, swap the left and right nodes, and put the left and right nodes back into the queue given they are not null.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
                
        if not root: return root

        queue = [root]

        while queue:
            cur = queue.pop()
            cur.left, cur.right = cur.right, cur.left
            if cur.left: queue.append(cur.left)
            if cur.right: queue.append(cur.right)

        return root
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 2: Using a Recursion

#### Implementation

The approach uses recursion. If the current node is not null, it will swap the left and right pointer while calling funciton itself to reverse further.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
                
        if root: root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
        return root
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)