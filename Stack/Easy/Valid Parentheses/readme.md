# Valid Parentheses

## Problem Link

[https://leetcode.com/problems/valid-parentheses/]

## Solutions

### Solution 1: [Using Stack]

#### Implementation

The approach uses a stack to keep track of parentheses. We push every opening paranthesis to the stack. Each time we encounter a closing parantheses, we pop the stack and match the pair.

```python
class Solution:
    def isValid(self, s: str) -> bool:
        
        pairs = {')':'(', ']': '[', '}': '{'}
        stack = []

        for c in s:
            if c in pairs:
                if not stack or stack.pop() != pairs[c]: return False
            else: stack.append(c)

        return not stack

```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)