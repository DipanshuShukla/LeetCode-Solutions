# Clone Graph

## Problem Link

[https://leetcode.com/problems/clone-graph]

## Solutions

### Solution 1: [Recursive DFS with HashMap]

To create a deep copy of an undirected graph, we must traverse every node and edge while avoiding infinite loops caused by cycles. 

We use a recursive Depth-First Search (DFS) alongside a `HashMap` that maps original nodes to their cloned counterparts. When we visit a node, we first check if it's already in our map. If so, we simply return the cloned reference to wire up the neighbors correctly. If not, we instantiate a new cloned node, immediately place it into the map to mark it as "visited," and then recursively clone all of its neighbors.

### Java

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {

        return cloneGraph(node, new HashMap<>());
    }

    public Node cloneGraph(Node node, Map<Node, Node> map){
        if (node == null) return null;
        if (map.containsKey(node)) return map.get(node);
        Node cloneNode = new Node(node.val);
        map.put(node, cloneNode);

        for (Node child: node.neighbors){
            Node cloneChild = cloneGraph(child, map);
            if (cloneChild != null) cloneNode.neighbors.add(cloneChild);
        }

        return cloneNode;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(N+E)
- **Space Complexity:** O(N)