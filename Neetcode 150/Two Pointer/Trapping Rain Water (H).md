## Question
Given an array of non-negative integers `height` which represent an elevation map. Each value `height[i]` represents the height of a bar, which has a width of `1`. 
Return the maximum area of water that can be trapped between the bars.

**Example 1**: 
![[Pasted image 20260719153303.png]]

```java
Input: height = [0,2,0,3,1,0,1,3,2,1]

Output: 9
```

## Solutions

### Calculating water for each `i` both ways
For each index `i` in the array, we need to find the max height to the left, and max height to the right. Then the water that can be held at position `i` would be the min of those two heights minus the height of the current position. If this is positive, it should be able to store the water.

#### Code
```python
        water = 0

        for i in range(len(height)):
            # Calculate the left max
            left_max = 0
            for j in range(0, i):
                left_max = max(left_max, height[j])

            # Calculate the right max
            right_max = 0
            for j in range(i + 1, len(height)):
                right_max = max(right_max, height[j])
            water += max(0, min(left_max, right_max) - height[i])

        return water
```
Time Complexity: $O(n^2)$
Space Complexity: $O(1)$

### Two Pointer Approach
