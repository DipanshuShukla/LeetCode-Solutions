# Same Tree

## Problem Link

https://leetcode.com/problems/same-tree/

## Solutions

### Solution 1: Recursive DFS Approach

#### Implementation
This solution uses a recursive approach, the function checks if any of the roots are null and returns if they are equal Otherise it returns if the root values are equal and then recursively calls the functions to compare the left and right nodes of both the roots.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p or not q: return p==q
        return p.val == q.val and self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(h), where h is the height of the tree

### Solution 2: Iterative DFS Approach

#### Implementation
This approach uses a Stack to traverse the tree. The stack stores tree node pairs. For each iteration the stack is poped and the resulting tree node pairs are compared. The result is returned accordingly.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        
        stack = [[p,q]]
        
        while stack:
            curp, curq = stack.pop()
            
            if curp == curq: continue
            if not curp or not curq or curp.val != curq.val: return False
            
            stack.append([curp.left, curq.left])
            stack.append([curp.right, curq.right])
        
        return True
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 3: Iterative BFS Approach

#### Implementation

This approach uses a Queue to traverse the tree. The queue stores tree node pairs. For each iteration the queue is poped and the resulting tree node pairs are compared. The result is returned accordingly.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        
        q = deque([[p,q]])
        
        while q:
            curp, curq = q.popleft()
            
            if curp == curq: continue
            if not curp or not curq or curp.val != curq.val: return False
            
            q.append([curp.left, curq.left])
            q.append([curp.right, curq.right])
        
        return True

```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)