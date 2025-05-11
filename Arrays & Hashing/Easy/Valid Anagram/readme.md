# Valid Anagram

## Problem Link

[https://leetcode.com/problems/valid-anagram/]

## Solutions

### Solution 1: [Sorting the Strings]

#### Implementation

For each character in s, try to find an unvisited matching character in t.
If all characters from s can be matched uniquely in t, they are anagrams.

### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        boolean[] visited = new boolean[s.length()];

        for (char c : s.toCharArray()){
            boolean found = false;
            for (int i = 0; i < t.length(); i++){
                if (t.charAt(i) == c && !visited[i]){
                    visited[i] = true;
                    found = true;
                    break;
                }
            }

            if (!found) return false;
        }

        return true;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(n)


### Solution 2: [Sorting the Strings]

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
- **Space Complexity:** O(1) (excluding sort space)

### Solution 3: [Using a HashMap]

#### Implementation

This approach uses two HashMaps data structure to track and count each character in each of the strings and then compares them in the end in python implementation.
In Java implementation we just populate a map using the first string with characters s as keys and their frequencies as values and then depopulate the map similarly keeping check that the count does not fall below 1. 

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

        for (char c : s.toCharArray()) map.put(c, map.getOrDefault(c,0) + 1);

        for (char c : t.toCharArray()){
            if (!map.containsKey(c) || map.get(c)<1) return false;

            map.put(c, map.get(c) - 1);
        }

        return true;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)


### Solution 4: [Using a 26 length array (for lowercase letters only)]

#### Implementation

Use a 26-length int array to track character frequencies.

### Java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] chars = new int[26];

        for (char c : s.toCharArray()) chars[c - 'a'] += 1;

        for (char c : t.toCharArray()){
            if (chars[c - 'a'] < 1) return false;
            
            chars[c - 'a'] -= 1; 
        }

        return true;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)