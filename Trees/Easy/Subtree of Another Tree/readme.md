# Subtree of Another Tree

## Problem Link

https://leetcode.com/problems/subtree-of-another-tree/

## Solutions

### Solution 1: Recursive DFS Approach

#### Implementation
This solution uses a recursive approach, it recursively call the SameTree Function on the tree during traversal in an  in order manner.
The SameTree function checks if any of the roots are null and returns if they are equal Otherise it returns if the root values are equal and then recursively calls the functions to compare the left and right nodes of both the roots.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root: return root == subRoot
        return self.isSameTree(root,subRoot) or self.isSubtree(root.left,subRoot) or self.isSubtree(root.right,subRoot)
        
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p or not q: return p==q
        return p.val == q.val and self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)
```

#### Complexity Analysis

- **Time Complexity:** O(n*m), where n is the number of nodes in root and m is the number of nodes in subRoot.
- **Space Complexity:** O(h), where h is the height of the recursion stack. In the worst case, it's O(n), where n is the number of nodes in the larger of the two trees.

### Solution 2: Preorder Serialization

#### Implementation

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        def serialize(root):
            if not root: return str(root)
            return '#' + str(root.val) + serialize(root.left) + serialize(root.right)

        return serialize(subRoot) in serialize(root)
```

#### Complexity Analysis

- **Time Complexity:** O(n+m)
- **Space Complexity:** O(n+m)
