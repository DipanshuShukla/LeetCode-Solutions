# Max Area of Island

## Problem Link

[https://leetcode.com/problems/max-area-of-island]

## Solutions

### Solution 1: [Iterative BFS]

Traverse the grid using two loops. Whenever a position for unvisited land is found we initialize and increment an island area variable and run iterative bfs starting from that position with help of a queue visiting all neighbours and incrementing the area.

To optimize space, we avoid using a separate `visited` array. Instead, we mutate the grid directly, changing the land (`1`) to water (`0`) as soon as we enqueue it. This "sinks" the island as we traverse it, ensuring we don't visit the same piece of land twice and saving space.

### Java

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int maxArea = 0;

        int[][] directions = {{-1,0}, {0,-1}, {1,0}, {0,1}};

        for (int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if (grid[i][j] == 1){
                    Queue<int[]> q = new LinkedList<>();
                    q.add(new int[]{i, j});

                    int curArea = 1;
                    grid[i][j] = 0;

                    while(!q.isEmpty()){
                        int[] curNode = q.poll();

                        for (int[] dir: directions){
                            int curX = curNode[0] + dir[0];
                            int curY = curNode[1] + dir[1];

                            if (curX >= 0 && curY >= 0 && curX < m && curY < n && grid[curX][curY] == 1){

                                curArea++;
                                grid[curX][curY] = 0;

                                q.add(new int[]{curX, curY});
                            }
                        }
                    }

                    maxArea = Math.max(maxArea, curArea);
                }
            }
        }
        
        return maxArea;

    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(M * N)
- **Space Complexity:** O(M * N)