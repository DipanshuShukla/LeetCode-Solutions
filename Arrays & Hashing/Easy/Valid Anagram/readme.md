# Valid Anagram

## Problem Link

[https://leetcode.com/problems/valid-anagram/]

## Solutions

### Solution 1: [Sorting the Strings]

#### Implementation

The approach sorts both the strings and then traverses both of them at the same time ensuring each character matches in both the stings

### Python

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:

        return sorted(s) == sorted(t)
```

### Java

```Java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        char[] sArr = s.toCharArray();
        char[] tArr = t.toCharArray();
        Arrays.sort(sArr);
        Arrays.sort(tArr);

        s= String.valueOf(sArr);
        t = String.valueOf(tArr);

        return s.equals(t);
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

### Solution 2: [Using a HashMap]

#### Implementation

This approach uses two HashMaps data structure to track and count each character in each of the strings and then compares them in the end.

### Python

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
### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        HashMap<Character, Integer> map = new HashMap<>();

        for (int i = 0; i < s.length(); i++) map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0)+1);

        for (int i = 0; i < t.length(); i++){
            if (!map.containsKey(t.charAt(i)) || map.get(t.charAt(i)) <1) return false;
            map.put(t.charAt(i), map.get(t.charAt(i))-1);
        }

        return true;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)