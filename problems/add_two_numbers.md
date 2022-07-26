## Question

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Solution

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

```python
   def addTwoNumbers(self, l1, l2):
        carry = 0
        prehead = ListNode()
        tail = prehead
        while l1 or l2 or carry:
            sum_ = carry
            if l1:
                sum_ += l1.val
                l1 = l1.next
            if l2:
                sum_ += l2.val
                l2 = l2.next

            carry, ans = divmod(sum_,10)
            tail.next = ListNode(ans)

            tail = tail.next

        return prehead.next
```
