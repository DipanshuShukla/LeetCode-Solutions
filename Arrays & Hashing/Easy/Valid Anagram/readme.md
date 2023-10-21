# Valid Anagram

## Problem Link

[https://leetcode.com/problems/valid-anagram/]

## Solutions

### Solution 1: [Sorting the Strings]

#### Implementation

The approach sorts both the strings and then traverses both of them at the same time ensuring each character matches in both the stings

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:

        return sorted(s) == sorted(t)
```

#### Complexity Analysis

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

### Solution 2: [Using a HashMap]

#### Implementation

This approach uses two HashMaps data structure to track and count each character in each of the strings and then compares them in the end.

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        
        if len(s) != len(t): return False

        smap,tmap = {},{}

        for i in range(len(s)):
            smap[s[i]] = smap.get(s[i],0) + 1
            tmap[t[i]] = tmap.get(t[i],0) + 1
        
        return smap == tmap
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)