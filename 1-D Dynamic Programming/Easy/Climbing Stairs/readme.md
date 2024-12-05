# Climbing Stairs

## Problem Link

https://leetcode.com/problems/climbing-stairs/

## Solutions

### Solution 1: Recursive Memoisation

#### Implementation

This approach uses recursive approach to traverse all possible subproblems of the problems. A Hash Map is employed as a cache to store and retrieve the results of already seen subproblems. This eliminates the need to calculate redundant subproblems.

```python
class Solution:
    def climbStairs(self, n: int, cache = {}) -> int:
        if n == 0: return 1
        if n<0: return 0

        if not n in cache: cache[n] = self.climbStairs(n-1, cache) + self.climbStairs(n-2, cache)
        return cache[n]
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 2: Tabulation

#### Implementation

This approach uses an array to store the number of ways to climb stairs. The indices of the array represents the stair number. We define the a few base cases till stare number 2 in the array. The rest are calculated as the sum of number of ways to climb the previous stair and stare before that.
i.e. s[n] = s[n-1]+s[n-2]. At the end we just return the last value of the array as the result.

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2: return n
            
        dp = [0]*(n+1)
        dp[1]=1
        dp[2]=2

        for i in range(3,n+1): dp[i] = dp[i-1]+dp[i-2]

        return dp[-1]
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 3: Tabulation without using extra space

#### Implementation

This approach is similar to the previous solution but, instead of an array, it uses two variables to store the number of ways to climb previous two stairs.

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 3: return n

        s1, s2 = 1, 2

        for i in range(3,n+1):
            cur = s2 + s1
            s1,s2 = s2,cur
        
        return s2
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

### Solution 4: Simplified Binet's Formula

#### Implementation

This approach uses a simplified form of Binet's formula to calculate the nth Fibonacci number in constant space and constant time. Since the climbStairs problem can be mapped to finding the nth Fibonacci number, this formula applies.

```python
import math

class Solution:
    def climbStairs(self, n: int) -> int:
        sqrt5 = math.sqrt(5)
        fib_n = math.pow((1 + sqrt5) / 2, n + 1) / sqrt5
        return round(fib_n)
```

#### Complexity Analysis

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)
