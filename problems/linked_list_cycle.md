## Question
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

## Solution
Use Floyd Warshall Algorithm. Fun Fact: This algorithm can also be used in finding Shorest Path.
O(1) memory = O(1) space : memory and space mean the same thing.
O(n) Time Complexity

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head
        fast = head
        
        while head is not None:
            try:
                slow = slow.next
                fast = fast.next.next
                if slow == fast:
                    return True
            except:
                return False
        return False
```
