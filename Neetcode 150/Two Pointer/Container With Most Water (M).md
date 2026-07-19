## Question
You are given an integer array `heights` where `heights[i]` represents the height of the ith bar. You may choose any two bars to form a container. Return the maximum amount of water a container can store.

**Example 1:**
![[Pasted image 20260719151142.png]]
```java
Input: height = [1,7,2,5,4,7,3,6]

Output: 36
```

**Example 2:**

```java
Input: height = [2,2,2]

Output: 4
```

## Solutions

### Brute Force Loop
We can iterate through all possible pairs and calculate the area for them. Through this, we can find the max.
#### Code
```cpp
        int currMax = 0;

        for (int i = 0; i < heights.size(); i++) {
            for (int j = i + 1; j < heights.size(); j++) {
                int currHeight = min(heights[i], heights[j]) * (j - i);
                currMax = max(currMax, currHeight);
            }
        }
        
        return currMax;
```

Time Complexity: $O(n^2)$
Space Complexity: $O(1)$

### Two Pointer Method
Instead of comparing all pairs, we can use a two pointer method and calculate the area each time. Once we calculate the area, we would just need to move the pointer with the shorter height.

#### Code
```python
        int low = 0;
        int high = heights.size() - 1;
        int maxHeight = 0;

        while (low < high) {
            int currHeight = min(heights[low], heights[high]) * (high - low);
            maxHeight = max(maxHeight, currHeight);
            if (heights[low] < heights[high]) {
                low++;
            }
            else {
                high--;
            }
        }

        return maxHeight;
```

Time Complexity: $O(n)$
Space Complexity: $O(n)$