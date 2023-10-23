# Two Sum

## Problem Link

[https://leetcode.com/problems/two-sum/]

## Solutions

### Solution 1: [Bruteforce Approach]

#### Implementation

The approach linearly traverses over the array and for each iteration linearly searches for the target sum pair in the remaining array.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i]+nums[j]==target: return [i,j]

```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### Solution 2: [Using a HashMap]

#### Implementation

This approach uses a HashMap data structure to keep track of visited elements. It checks, for each element in the array, whether the complement (target minus the current element) is present in the hashmap.


```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        map = {}

        for i in range(len(nums)):
            if target-nums[i] in map: return [i,map[target-nums[i]]]
            map[nums[i]]=i
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)