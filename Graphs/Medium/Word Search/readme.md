# Word Search

## Problem Link

[https://leetcode.com/problems/word-search]
## Solutions

### Solution 1: DFS with Backtracking (In-Place)

We traverse the grid looking for the first character of the target word. When we find a match, we launch a recursive Depth-First Search (DFS) to locate the subsequent characters.

To handle backtracking and avoid revisiting the same cell within a single traversal path, we must mark cells as "visited." To optimize space, we temporarily mutate the current cell on the board to a special character (`#`). After the recursive calls for that cell finish, we restore the original character. This allows us to backtrack efficiently without allocating an $O(M \times N)$ boolean matrix.

### Java

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length, n = board[0].length;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word.charAt(0)) {
                    char originalChar = board[i][j];
                    board[i][j] = '#';
                    if (exist(board, word, 0, new int[]{i, j})) return true;
                    board[i][j] = originalChar;
                }
            }
        }

        return false;
    }
    
    public boolean exist(char[][] board, String word, int charIndex, int[] pos) {
        if (charIndex == word.length() - 1) return true;

        int[][] directions = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};

        for (int[] dir : directions) {
            int curX = pos[0] + dir[0];
            int curY = pos[1] + dir[1];

            if (curX >= 0 && curY >= 0 && curX < board.length && curY < board[0].length && board[curX][curY] != '#') {
                char originalChar = board[curX][curY];
                if (originalChar != word.charAt(charIndex + 1)) continue;
                
                board[curX][curY] = '#';
                boolean res = exist(board, word, charIndex + 1, new int[]{curX, curY});
                if (res) return res;
                board[curX][curY] = originalChar;
            }
        }

        return false;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(M * N * (3 ^ L)), where L = length of word
- **Space Complexity:** O(L)