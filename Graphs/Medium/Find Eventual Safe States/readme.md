# Find Eventual Safe States

## Problem Link

[https://leetcode.com/problems/find-eventual-safe-states]

## Solutions

### Solution 1: [Recursive DFS]

We use recursion to make use of the call stack to carry out a dfs search marking each node visited along the way using a simple for loop. 

We use a `Boolean` object array to track three distinct states for each node:
1. `null` -> Unvisited.
2. `false` -> Visiting (currently in the recursion stack) OR proven unsafe (leads to a cycle).
3. `true` -> Safe (all paths lead to a terminal node).

The main algorithm just loops over the given adjacency list and just invokes the  recursive dfs method to traverse all connected nodes as visited and safe/unsafe for memoization.

### Java

```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int n = graph.length;
        Boolean[] visitedSafety = new Boolean[n];
        List<Integer> res = new ArrayList<>();

        for (int i = 0; i < n; i++){
            if (isSafe(i, graph, visitedSafety)) res.add(i);
        }

        return res;
    }

    public boolean isSafe(int curNode, int[][] graph, Boolean[] visitedSafety){
        if (visitedSafety[curNode] != null) return visitedSafety[curNode];

        visitedSafety[curNode] = false;
        boolean res = true;

        for (int node: graph[curNode]) res = res && isSafe(node, graph, visitedSafety);
        visitedSafety[curNode] = res;
        return res;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n+E)
- **Space Complexity:** O(n)