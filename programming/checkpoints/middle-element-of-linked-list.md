# Middle element of linked list

https://www.interviewbit.com/problems/middle-element-of-linked-list/

Given a linked list of integers. Find and return the middle element of the linked list.

Note: If there are N nodes in the linked list and N is even then return the (N/2+1)th element.

```
Input Format

The only argument given head pointer of linked list.
Output Format

Return the middle element of the linked list.
Constraints

1 <= length of the linked list <= 100000
1 <= Node value <= 10^9 
For Example

Input 1:
    1->2->3->4->5
Output 1:
   3 

Input 2:
    A = 1->5->6->2->3->4
Output 2:
    2
```

## Solution

### Editorial
```cpp
int Solution::solve(ListNode* A) {
    ListNode* slow=A;
    ListNode* fast=A;
    while(fast!=NULL && fast->next!=NULL)
    {
        fast=fast->next->next;
        slow=slow->next;
    }
    return slow->val;
}
```

### Fastest
```cpp
int Solution::solve(ListNode* A) {
    ListNode* slow=A;
    ListNode* fast=A;
    while(fast!=NULL && fast->next!=NULL)
    {
        fast=fast->next->next;
        slow=slow->next;
    }
    return slow->val;
}
```

### Lightweight
```cpp
int Solution::solve(ListNode* A) {
    ListNode* slow=A;
    ListNode* fast=A;
    while(fast&&fast->next)
    {
        slow=slow->next;
        fast=fast->next->next;
    }
    return slow->val;
}
```

