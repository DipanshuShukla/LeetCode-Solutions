# Number of 1 Bits

## Problem Link

https://leetcode.com/problems/number-of-1-bits/

## Solutions

### Solution 1: Using Bitwise AND operator and right shifting

#### Implementation

In this approach while the number exists, we use bitwise AND
operator to count a 1 at right most position and keep right shifting bits.

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0

        while n:
            res += n&1
            n >>= 1

        return res
```

#### Complexity Analysis

- **Time Complexity:** O(32), since the input will always be 32 bit unsigned integer string.
- **Space Complexity:** O(1)

### Solution 2: Using Brian Kernighan’s Algorithm

#### Implementation

This algorithm works by repeatedly flipping the rightmost set bit of the number to zero until the number becomes zero. It leverages the property that n & (n - 1) flips the rightmost set bit to zero.

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0

        while n:
            n &= n-1
            res += 1
            
        return res
```

#### Complexity Analysis

- **Time Complexity:** O(k), where k is the number of set bits in the integer.
- **Space Complexity:** O(1)
