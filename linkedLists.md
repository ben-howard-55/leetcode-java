# Linked List Data Structure

## LeetCode Questions

[TOC]

---

### Reverse Linked List (recursive)

16-01-2021

#### constraints

~~~
Reverse a singly linked list. (recursively)
~~~

#### Code Solution

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { 
 *				this.val = val; this.next = next; 
 *		 }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) return null;
        
        return recursive(head, null);
    }
    
    public ListNode recursive(ListNode node, ListNode next) {
        ListNode node1 = new ListNode(node.val, next);
        
        if (node.next != null) {
            return recursive(node.next, node1);  
        } else {
            return node1;
        }
    }
}
```

####  Explanation of Solution

The recursive functions is passed two things:

1) the current node 

2) the next node.  

The initial node is `head`and next is `null` because due to the recursive nature of the function a new node will be created, in which has the value of the head and the next pointing towards null.

This new node is then passed again into the recursive function as the `next` node, and the original `next` of the node is passed as the current `node`. 

This recursive pattern repeats until a null next is found and then stops and returns the last next `ListNode`.

---

