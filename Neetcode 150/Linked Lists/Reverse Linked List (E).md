## Question
Given the beginning of a singly linked list `head`, reverse the list, and return the new beginning of the list.

**Example 1:**

```java
Input: head = [0,1,2,3]

Output: [3,2,1,0]
```

**Example 2:**

```java
Input: head = []

Output: []
```

## Solution

### Using prev, curr, next pointers

Setting prev to None and curr to the head, we can start a while loop and terminate when current is None. Inside, we change current.next to prev and shift each node down. Doing this until current is null would make prev the new head of the list.

#### Code
```python
        if not head or not head.next:
            return head
  
        curr = head
        prev = None

        while curr:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next

        return prev
```
Time Complexity: $O(n)$
Space Complexity: $O(1)$
