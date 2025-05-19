# Linked List Cycle

## Problem Link

[https://leetcode.com/problems/linked-list-cycle/]

## Solutions

### Solution 1: Using a HashMap to track visited Nodes

#### Implementation

The approach uses a HashMap to keep track of visited nodes while traversing the linked list linearly. If the current node is already present in the HashMap, it is clear we have detected a cycle. If the end of linked list is reached, we return False.

### Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        cur = head
        cache = {}

        while cur:
            if cur in cache: return True
            cache[cur] = cur
            cur = cur.next

        return False
```

### Java

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        
        HashSet<ListNode> set = new HashSet<>();

        while(head!=null){
            if (set.contains(head)) return true;
            set.add(head);
            head = head.next;
        }

        return false;

    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)


### Solution 2: Using Slow-Fast Pointer (Hare and Tortoise Technique)

#### Implementation

The approach uses a fast and a slow pointer to traverse the list. The slow pointer traveses one node at a time and fast pointer traverses twise the speed of slow pointer. If the pointers meet we have detected a cycle. On the other hand, if the fast pointer reaches the end of the list it signifies that there are no cycles.

### Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head

        while fast and fast.next:
            slow=slow.next
            fast = fast.next.next
            if slow == fast: return True

        return False
```

### Java

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        
        ListNode slow = head, fast = head;

        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if (fast == slow) return true;
        }

        return false;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

### Solution 3: Modifying Nodes In-Place to mark visited

#### Implementation

The approach modifies the value of the visited nodes to detect them later as visited.

### Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:

        while head:
            if head.val == float('inf'): return True
            head.val = float('inf')
            head = head.next

        return False
```

### Java

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        
        while(head != null){
            if (head.val == Integer.MAX_VALUE) return true;
            head.val = Integer.MAX_VALUE;
            head = head.next;
        }

        return false;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
