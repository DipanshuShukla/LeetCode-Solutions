# Invert Binary Tree

## Problem Link

https://leetcode.com/problems/invert-binary-tree/

## Solutions

### Solution 1: Using a queue [Level order Traversal, iterative bfs]

#### Implementation

The method uses an iterative approach and uses a queue to traverse a tree. We start to traverse a queue containing the root node in the begining. During each iteration, we swap the left and right node of the current node popped from the queue, and put the left and right nodes back into the queue given they are not null.

### Python

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

### Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {

        if (root == null) return root;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()){

            TreeNode cur = queue.poll();

            TreeNode temp = cur.left;
            cur.left = cur.right;
            cur.right = temp;

            if (cur.left != null) queue.add(cur.left);
            if (cur.right != null) queue.add(cur.right);
        }

        return root;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(w), w = width of the tree.

### Solution 2: Using a Recursive DFS

#### Implementation

The approach uses recursion. If the current node is not null, it will swap the left and right pointer while calling funciton itself to reverse further.

### Python

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

### Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root != null){
            TreeNode temp = this.invertTree(root.left);
            root.left = this.invertTree(root.right);
            root.right = temp;
        }

        return root;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(h), where h is the height of the tree (because of the call stack)


### Solution 3: Using a stack [Iterative DFS]

#### Implementation

The method uses an a stack to traverse the tree in DFS fashion.

### Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;

        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while(!stack.isEmpty()){
            TreeNode cur = stack.pop();
            TreeNode temp = cur.left;
            cur.left = cur.right;
            cur.right = temp;

            if (cur.right != null) stack.push(cur.right);
            if (cur.left != null) stack.push(cur.left);
        }

        return root;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(h), where h is the height of the tree

### Solution 4: Using a stack [Recursive BFS]

#### Implementation

The method uses an a recursive approach to traverse the tree in BFS fashion. we take the length of the current level at the begining to traverse only the nodes in the current level.

### Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return root;

        Queue<TreeNode> q = new LinkedList();
        q.add(root);

        invertTree(q);

        return root;
    }

    public void invertTree(Queue<TreeNode> q) {
        if (q.isEmpty()) return;
        int curLen = q.size();

        for (int i = 0; i < curLen; i++){
            TreeNode cur = q.poll();

            TreeNode temp = cur.left;
            cur.left = cur.right;
            cur.right = temp;

            if (cur.left != null) q.add(cur.left);
            if (cur.right !=  null) q.add(cur.right);
        }

        invertTree(q);
    }

}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(w), w = width of the tree.
