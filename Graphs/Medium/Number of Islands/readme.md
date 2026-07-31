# Number of Islands

## Problem Link

[https://leetcode.com/problems/number-of-islands]

## Solutions

### Solution 1: [Iterative BFS]

Traverse the grid using two loops. Whenever a position for unvisited land is found we increment the island count and run iterative bfs starting from that position with help of a queue marking all it's adjacent lands visited.
To optimize space, we avoid using a separate `visited` array. Instead, we mutate the grid directly, changing the land (`'1'`) to water (`'0'`) as soon as we enqueue it. This "sinks" the island as we traverse it, ensuring we don't visit the same piece of land twice and saving space.

### Java

```java
class Solution {
    public int numIslands(char[][] grid) {
        int m = grid.length, n = grid[0].length;
        int islandCount = 0;

        for (int i = 0; i < m; i++){
            for (int j = 0 ; j < n; j++){
                if (grid[i][j] == '1'){
                    islandCount++;

                    Queue<int[]> q = new LinkedList<>();
                    q.add(new int[]{i,j});
                    grid[i][j] = '0';

                    bfs(q, grid);
                }
            }
        }

        return islandCount;
    }

    private void bfs(Queue<int[]> q, char[][] grid){

        int[][] directions = {{-1,0},{0,-1},{+1,0},{0,+1}};

        while(!q.isEmpty()){
            int[] curNode = q.poll();

            for (int[] dir: directions){
                int curX = curNode[0] + dir[0];
                int curY = curNode[1] + dir[1];
                if(curX >= 0 && curX < grid.length && curY >= 0 && curY < grid[0].length && grid[curX][curY] == '1'){
                    grid[curX][curY] = '0';
                    q.add(new int[]{curX,curY});
                }
            }
            
        }
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(M * N)
- **Space Complexity:** O(M * N)