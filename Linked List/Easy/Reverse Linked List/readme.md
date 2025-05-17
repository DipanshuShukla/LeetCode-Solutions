# Reverse Linked List

## Problem Link

[https://leetcode.com/problems/reverse-linked-list/]

## Solutions

### Solution 1: [Using Recursion]

#### Implementation

The approach uses recursion to first traverse to the end of the list to find the Head of the new Linked List and save it in a variable to return later. Now, the list is reversed before returning.

### Python

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

### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {

        if (head == null || head.next == null) return head;

        ListNode res = reverseList(head.next);
        
        head.next.next =  head;
        head.next = null;

        return res;   
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### Solution 2: [Using Recursion with refrence variable]

#### Implementation

This approach is the same as the recursive approach but uses a refrence variable to pass in the recurison funciton that decreases the space complexity.

### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

    class ResultWrapper{
        ListNode result;
    }

    public void reverseList(ListNode head, ResultWrapper resultWrapper) {
        if (head == null || head.next == null) {
            resultWrapper.result = head;
            return;
        }
        reverseList(head.next, resultWrapper);
        head.next.next =  head;
        head.next = null;
    }

    public ListNode reverseList(ListNode head) {

        ResultWrapper resultWrapper = new ResultWrapper();

        reverseList(head, resultWrapper);

        return resultWrapper.result;
        
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n) not truly O(1) space due to call stack


### Solution 3: [Using While-Loop]

#### Implementation

The approach uses a while loop to traverse the linked list linearly to the end. For each iteration of the while loop, we save the next node to a temp variable, update the current node to point to the previous node, update the previous node to the current node, update the current node to the node saved in the temp vaiable and continue the loop. when the loop exits, we return whatever is stored in the previous node.

### Python

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

### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {

        ListNode cur = head, prev = null;
        
        while(cur != null){
            ListNode temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }
}

```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

### Solution 4: [Using Stack]

#### Implementation

This approach uses a stack to so the same we did with the recursion call stack.

### Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;

        Stack<ListNode> stack = new Stack<>();

        while(head !=null){
            stack.push(head);
            head = head.next;
        }

        head = stack.pop();
        head.next = null;

        while(!stack.isEmpty()){
            ListNode cur = stack.pop();
            cur.next.next = cur;
            cur.next = null;
        }

        return head;
    }
}
```

#### Complexity Analysis

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)
