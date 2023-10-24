# Valid Palindrome

## Problem Link

[https://leetcode.com/problems/valid-palindrome/]

## Solutions

### Solution 1: [Left-Right Pointer]

#### Implementation

The approach uses two pointers (one left, one right) to check for palindrome from both sides while ignoring special characters.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        
        l,r = 0, len(s)-1

        while l<r:
            while not (s[l].isalpha() or s[l].isdigit()) and l<r: l+=1
            while not (s[r].isalpha() or s[r].isdigit()) and l<r: r-=1
            if l>r: break
            
            if s[l].lower() != s[r].lower(): return False
            l+=1
            r-=1

        return True
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

### Solution 2: [Creating new filtered string and then using Left-Right Pointer]

#### Implementation

This approach first creates a new string by filtering all special characters from the orignal string. After filtering it uses the same two pointer technique as the previous solution.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:

        newS = ''
        l,r = 0, len(newS)-1

        for c in s:
            if c.isalpha() or c.isdigit(): newS += c.lower()

        return newS == newS[::-1]
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)