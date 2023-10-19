# Contains Duplicate

## Problem Link

[https://leetcode.com/problems/contains-duplicate/]

## Solutions

### Solution 1: [Bruteforce Approach]

#### Implementation

The approach linearly traverses over the array and for each iteration linearly searches for a duplicate in the remaining array.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:

        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i]==nums[j]: return True

        return False
```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### Solution 2: [Using Sorting]

#### Implementation

This approach sorts the array and then linearly traverses the new sorted array to compare the adjacent elements for duplicates.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:

        nums.sort()

        for i in range(len(nums)-1):
            if nums[i]==nums[i+1]: return True

        return False
```

#### Complexity Analysis

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

### Solution 3: [Using a HashMap]

#### Implementation

This approach uses a HashMap data structure to keep track of visited elements and checks for duplicates every iteration of traversal.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:

        map = {}

        for i in range(len(nums)):
            if nums[i] in map: return True
            map[nums[i]]=i
            
        return False
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)