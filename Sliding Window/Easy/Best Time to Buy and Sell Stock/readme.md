# Best Time to Buy and Sell Stock

## Problem Link

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/]

## Solutions

### Solution 1: [Bruteforce Approach]

#### Implementation

The approach uses nested loops to traverse the array and, for each iteration, calculates the profit for all possible sell days after the current buy day to find the maximum profit.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:

        maxProfit = 0

        for i in range(len(prices)):
            for j in range(i + 1, len(prices)):
                maxProfit = max(maxProfit, prices[j] - prices[i])

        return maxProfit

```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### Solution 2: [Left-Right Pointer]

#### Implementation

The approach uses two pointers one left to keep track of the lowest price encountered, one right to traverse the list and keep updating the max-profit.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        
        lowest = prices[0]
        maxP = 0

        for current in prices:
            if lowest > current: lowest = current
            else: maxP = max(maxP, current-lowest)

        return maxP
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
