# Rotting Oranges

## Problem Link

[https://leetcode.com/problems/rotting-oranges]

## Solutions

### Solution 1: [Iterative BFS]

We use a multi-source Breadth-First Search (BFS) to model the rotting process minute by minute. First, we iterate through the grid to count all fresh oranges and enqueue the starting positions of all rotten oranges. 

During the BFS, we process the queue level-by-level by capturing the queue's size at the start of each iteration. For each rotten orange, we check its four adjacent neighbors using a direction array. If a neighbor is a fresh orange, we rot it (updating the grid in place), decrement our fresh orange count, and add it to the queue for the next minute. We use a boolean flag, `rottedThisMinute`, to ensure we only increment our time counter if actual rotting occurred during that level. Finally, if the fresh orange count reaches 0, we return the total minutes elapsed; otherwise, we return `-1`.

### Java

```java
class Solution {
    public int orangesRotting(int[][] grid) {

        int m = grid.length, n = grid[0].length;

        int freshOrangeCount = 0;

        Queue<int[]> q = new LinkedList<>();
        
        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                if (2 == grid[i][j]){
                    q.add(new int[]{i,j});
                }
                if (1 == grid[i][j]) freshOrangeCount++;
            }
        }

        return bfs(q, grid, freshOrangeCount);
        
    }

    private int bfs(Queue<int[]> q, int[][] grid, int freshOrangeCount){
        int curMinute = 0;

        int[][] directions = {{-1,0},{0,-1},{+1,0},{0,+1}};

        while(!q.isEmpty()){
            boolean rottedThisMinute = false;
            int curSize = q.size();
            for (int i = 0; i < curSize; i++){
                int[] curOrange = q.poll();
                for (int[] dir: directions){
                    int row = curOrange[0] + dir[0];
                    int col = curOrange[1] + dir[1];

                    if(row >= 0 && col >= 0 && row < grid.length && col < grid[0].length && 1 == grid[row][col]){
                        grid[row][col] = 2;
                        rottedThisMinute = true;
                        freshOrangeCount--;
                        q.add(new int[]{row, col});
                    }
                }
            }
            if (rottedThisMinute) curMinute++;
        }

        return 0 == freshOrangeCount ? curMinute : -1;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(M * N)
- **Space Complexity:** O(M * N)