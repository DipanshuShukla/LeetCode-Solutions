# Keys and Rooms

## Problem Link

[https://leetcode.com/problems/keys-and-rooms]

## Solutions

### Solution 1: [Iterative BFS]

We make use of a queue that we initialize with room 0 and mark node 0 as visited to iteratively traverse the graph in a bfs fashion. For each iteration a room is popped from the queue and their connnected nodes put into the queue and marked as visited. 
At the end the visited array is traversed linearly to check if all the rooms have been visited. In case we discover any node unvisited we return a false otherwise funtion returns true by default.

### Java

```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        
        int n = rooms.size();
        boolean[] visited = new boolean[n];

        Queue<Integer> q = new LinkedList<Integer>();
        q.add(0);
        visited[0] = true;

        bfs(q, rooms, visited);

        for (boolean roomVisted: visited){
            if (roomVisted == false) return false;
        }

        return true;
    }

    public void bfs(Queue<Integer> q, List<List<Integer>> rooms, boolean[] visited){

        while(q.size() != 0){
            Integer curNode = q.poll();
            
            for (Integer node: rooms.get(curNode)){
                if (visited[node] == false){
                    visited[node] = true;
                    q.add(node);
                }
                
            }
        }
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n+E)
- **Space Complexity:** O(n)


