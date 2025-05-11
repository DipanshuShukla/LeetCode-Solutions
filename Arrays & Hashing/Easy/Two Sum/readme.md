# Two Sum

## Problem Link

[https://leetcode.com/problems/two-sum/]

## Solutions

### Solution 1: [Bruteforce Approach]

#### Implementation

The approach linearly traverses over the array and for each iteration linearly searches for the target sum pair in the remaining array.

### Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i]+nums[j]==target: return [i,j]

```

### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        
        for (int i = 0; i < nums.length; i++)
            for (int j = i+1; j<nums.length; j++)
                if (nums[i] + nums[j] == target) return new int[]{i,j};

        return new int[]{};
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### Solution 2: [Using a HashMap]

#### Implementation

This approach uses a HashMap data structure to keep track of visited elements. It checks, for each element in the array, whether the complement (target minus the current element) is present in the hashmap.

### Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        map = {}

        for i in range(len(nums)):
            if target-nums[i] in map: return [i,map[target-nums[i]]]
            map[nums[i]]=i
```

### Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++){
            if (map.containsKey(target - nums[i]))
                return new int[]{i, map.get(target - nums[i])};
            map.put(nums[i], i);
        } 

        return new int[]{};
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)