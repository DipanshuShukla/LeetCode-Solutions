# Merge Two Sorted Lists

## Problem Link

[https://leetcode.com/problems/merge-two-sorted-lists/]

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
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        
        if not list1: return list2
        if not list2: return list1

        if list1.val > list2.val: list1,list2 = list2,list1

        list1.next = self.mergeTwoLists(list1.next,list2)

        return list1
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)


### Solution 2: [Using While-Loop]

#### Implementation

The approach uses a while loop to traverse the linked lists linearly until one of them ends, during each iteration we compare list head node values and attach the smaller one to a new dummy list.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        
        dummy = ListNode()
        cur = dummy

        while list1 and list2:
            if list1.val < list2.val:
                cur.next = list1
                list1 = list1.next
            else:
                cur.next = list2
                list2 = list2.next
            cur = cur.next
        
        cur.next = list1 or list2

        return dummy.next
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
