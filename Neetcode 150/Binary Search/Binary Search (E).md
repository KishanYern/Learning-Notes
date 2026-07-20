## Question
You are given an array of **distinct** integers `nums`, sorted in ascending order, and an integer `target`.

Implement a function to search for `target` within `nums`. If it exists, then return its index, otherwise, return `-1`.

Your solution must run in O(logn) time.

**Example 1:**

```java
Input: nums = [-1,0,2,4,6,8], target = 4

Output: 3
```

**Example 2:**

```java
Input: nums = [-1,0,2,4,6,8], target = 3

Output: -1
```

## Solution
### Binary Search
Simple binary search

#### Code
```cpp
        int low = 0;
        int high = nums.size() - 1;

        while (low <= high) {
            int mid = (low + high) / 2;
            cout << mid << endl;
            if (target == nums[mid]) {
                return mid;
            }
            else if (target > nums[mid]) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }

        return -1;
```

Time Complexity: $O(logn)$
Space Complexity: $O(1)$