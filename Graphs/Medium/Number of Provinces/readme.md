# Number of Provinces

## Problem Link

[https://leetcode.com/problems/number-of-provinces/]

## Solutions

### Solution 1: [Recursive DFS]

We use recursion to make use of the call stack to carry out a dfs search marking each node visited along the way using a simple for loop. the main algorithm just loops over the given adjacency matrix and just increments the province count whenever a non visited node is found then invoke the dfs method to mark all connected nodes as visited essentially considering those a part of current province.

### Java

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {

        int n = isConnected.length; // number of nodes
        int[] visited = new int[n];

        int count = 0; // number of provinces

        for (int i = 0; i < n; i++){
            if (visited[i] == 1) continue;
            count++;
            dfs(i, isConnected, visited);
        }

        return count;

    }

    private void dfs(int curNode, int[][] isConnected, int[] visited){
        visited[curNode] = 1;
        for (int j = 0; j < isConnected.length; j++){
                if (isConnected[curNode][j] == 1 && visited[j] == 0){
                    dfs(j, isConnected, visited);
                }
            } 
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(n)