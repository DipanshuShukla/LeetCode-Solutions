

# Serialize and Deserialize Binary Tree

## Problem Link

[https://leetcode.com/problems/serialize-and-deserialize-binary-tree/](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

## Solutions

### Solution 1: \[Level Order Traversal (BFS) using Queue]

#### Idea

* Use level-order traversal (BFS) to serialize the tree.
* Represent null nodes as "\*" to preserve structure.
* Use a space-separated string to store serialized values.
* For deserialization, read values left to right while building the tree level by level.

---

#### Java

```java
import java.util.StringJoiner;
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {

        if (root == null) return "";

        StringJoiner joiner = new StringJoiner(" ");

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            TreeNode cur = q.poll();
            if (cur == null) {
                joiner.add("*");
                continue;
            }
            joiner.add(Integer.toString(cur.val));
            q.add(cur.left);
            q.add(cur.right);
        }

        return joiner.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.isEmpty()) return null;

        String[] vals = data.split(" ");
        TreeNode root = new TreeNode(Integer.parseInt(vals[0]));
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        int i = 1;

        while (!q.isEmpty() && i < vals.length) {
            TreeNode cur = q.poll();

            if (!vals[i].equals("*")) {
                cur.left = new TreeNode(Integer.parseInt(vals[i]));
                q.add(cur.left);
            }

            if (i == vals.length - 1) break;
            i++;

            if (!vals[i].equals("*")) {
                cur.right = new TreeNode(Integer.parseInt(vals[i]));
                q.add(cur.right);
            }

            i++;
        }

        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```

---

#### Complexity Analysis

* **Time Complexity:**

  * Serialize: O(n)
  * Deserialize: O(n)
    where n is the number of nodes in the tree.

* **Space Complexity:** O(n)

  * For the queue and resulting string structure.
