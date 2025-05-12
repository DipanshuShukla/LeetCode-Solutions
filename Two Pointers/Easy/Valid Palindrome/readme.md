# Valid Palindrome

## Problem Link

[https://leetcode.com/problems/valid-palindrome/]

## Solutions

### Solution 1: [bruteforce approach]

#### Implementation

This approach first creates a new string by lowercasing the characters and filtering all special characters from the orignal string. After filtering it we compare from the natural string reverse.

### Python

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        newS = ''.join(c.lower() for c in s if c.isalnum())
        return newS == newS[::-1]

```

### Java

```java
class Solution {
    public boolean isPalindrome(String s) {

        s = s.toLowerCase().replaceAll("[^A-Za-z0-9]", "");

        return s.equals(new StringBuilder(s).reverse().toString());
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)


### Solution 2: [Left-Right Pointer]

#### Implementation

The approach uses two pointers (one left, one right) to check for palindrome from both sides while ignoring special characters.

### Python

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

### Java

```java
class Solution {
    public boolean isPalindrome(String s) {

        s = s.toLowerCase();

        int i = 0, j = s.length() - 1;
        
        while(i<j){
            while (!Character.isLetterOrDigit(s.charAt(i)) && i<j) i++;
            while (!Character.isLetterOrDigit(s.charAt(j)) && i<j) j--;

            if (s.charAt(i) != s.charAt(j)) return false;

            i++;
            j--;
        }

        return true;
    }
}

```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)