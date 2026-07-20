## Question
You are given an `m x n` 2-D integer array `matrix` and an integer `target`.

- Each row in `matrix` is sorted in _non-decreasing_ order.
- The first integer of every row is greater than the last integer of the previous row.

Return `true` if `target` exists within `matrix` or `false` otherwise.

Can you write a solution that runs in `O(log(m * n))` time?

**Example 1:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/7ca61f56-00d4-4fa0-26cf-56809028ac00/public)

```java
Input: matrix = [[1,2,4,8],[10,11,12,13],[14,20,30,40]], target = 10

Output: true
```

**Example 2:**

![](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/f25f2085-ce04-4447-9cee-f0a66c32a300/public)

```java
Input: matrix = [[1,2,4,8],[10,11,12,13],[14,20,30,40]], target = 15

Output: false
```

## Solutions
### Brute Force
Just scan through the whole matrix to find the target.
#### Code
```python
for m in range(len(matrix)):
	for n in range(len(matrix)):
		if matrix[m][n] == target:
			return True

return False
```
Time Complexity: $O(n^2)$
Space Complexity: $O(1)$
### Binary Search
Since each column has the property that the first integer in every row is greater than the last integer on the previous row (the first integer on a row is greater than everything before it), we can simplify the search by using binary search on the columns, then narrow it down to a row, then use a binary search to find it within the row.

The tricky part is noticing that if the target is greater than the mid row's first element, then the element can still be on that row.

#### Code
```python
        top, bot = 0, len(matrix) - 1
        row = -1
        while top <= bot:
            mid = (top + bot) // 2
            if (matrix[mid][0] <= target <= matrix[mid][-1]):
                row = mid
                break
            elif (matrix[mid][0] < target):
                top = mid + 1
            else:
                bot = mid - 1
                
        low, high = 0, len(matrix[0]) - 1
        while low <= high:
            mid = (low + high) // 2
            if matrix[row][mid] == target:
                return True
            elif matrix[row][mid] < target:
                low = mid + 1
            else:
                high = mid - 1
                
        return False
```

Time Complexity: $O(log(n*m))$
Space Complexity: $O(1)$