## Question
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** linked list and return the head of the new sorted linked list.

The new list should be made up of nodes from `list1` and `list2`.
**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/51adfea9-493a-4abb-ece7-fbb359d1c800/public)

```java
Input: list1 = [1,2,4], list2 = [1,3,5]

Output: [1,1,2,3,4,5]
```

**Example 2:**

```java
Input: list1 = [], list2 = [1,2]

Output: [1,2]
```

**Example 3:**

```java
Input: list1 = [], list2 = []

Output: []
```

## Solution

### Merge 
Same as class

#### Code
```cpp
        if (!list1) {
            return list2;
        }

        if (!list2) {
            return list1;
        }

        ListNode* newlist = nullptr;

        if (list1->val < list2->val) {
            newlist = list1;
            list1 = list1->next;
        }
        else{
            newlist = list2;
            list2 = list2->next;
        }

        ListNode* curr = newlist;

        while (list1 && list2) {
            if (list1->val < list2->val) {
                curr->next = list1;
                list1 = list1->next;
            }
            else {
                curr->next = list2;
                list2 = list2->next;
            }
            curr = curr->next;
        }

        if (list1 && (!list2)) {
            curr->next = list1;
        }
        else if (list2 && (!list1)){
            curr->next = list2;
        }

        return newlist;

    }
```