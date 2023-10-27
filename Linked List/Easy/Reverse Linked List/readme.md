# Reverse Linked List

## Problem Link

[https://leetcode.com/problems/reverse-linked-list/]

## Solutions

### Solution 1: [Using Recursion]

#### Implementation

The approach uses recursion to first traverse to the end of the list to find the Head of the new Linked List and save it in a variable to return later. Now, the list is reversed before returning.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next: return head

        res = self.reverseList(head.next)

        head.next.next = head
        head.next = None

        return res
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)


### Solution 2: [Using While-Loop]

#### Implementation

The approach uses a while loop to traverse the linked list linearly to the end. For each iteration of the while loop, we save the next node to a temp variable, update the current node to point to the previous node, update the previous node to the current node, update the current node to the node saved in the temp vaiable and continue the loop. when the loop exits, we return whatever is stored in the previous node.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head

        while cur:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
        
        return prev
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
