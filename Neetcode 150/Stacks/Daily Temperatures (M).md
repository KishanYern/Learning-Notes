## Question
You are given an array of integers `temperatures` where `temperatures[i]` represents the daily temperatures on the `ith` day.
Return an array `result` where `result[i]` is the number of days after the `ith` day before a warmer temperature appears on a future day. If there is no day in the future where a warmer temperature will appear for the `ith` day, set `result[i]` to `0` instead.

**Example 1:**

```java
Input: temperatures = [30,38,30,36,35,40,28]

Output: [1,4,1,2,1,0,0]
```

**Example 2:**

```java
Input: temperatures = [22,21,20]

Output: [0,0,0]
```

## Solution
### Stack approach
We will use a stack to store each number and its index in the given array. for each number:
1. if the stack is empty, add the number and its index in the stack.
2. else, we will keep going through the stack until we reach an empty stack, or we reach a temp that is higher than our own (temp in the past). for each temp that is lower, we would update our result array with the distance of their indices. 
3. At the end, we will add our number/index to the stack.

#### Code
```python
        res = [0 for _ in range(len(temperatures))]
        stack = []
        
        for i, num in enumerate(temperatures):
            if (len(stack) == 0):
                stack.append((num, i))
                continue

            while len(stack) and (num > stack[-1][0]):
                top_num, top_idx = stack.pop()
                res[top_idx] = i - top_idx
                
            stack.append((num, i))

        return res
```

Time Complexity: $O(n)$
Space Complexity: $O(n)$
