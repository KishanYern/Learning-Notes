## Question
Given an integer array `nums`, return all triplets `[nums[i], nums[j], nums[k]` where `nums[i] + nums[j] + nums[k] == 0`, and the indices i, j, k are all distinct. 
The output should not contain any duplicate triplets. You may return the output and the triplets in any order.

**Example 1:**
```java
Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]
```

**Example 2**:
```java
Input: nums = [0,1,1]

Output: []
```

## Solutions

### Brute Force
We can do a triple for loop and add triplets into the array. We should sort the array to be more efficient. To prevent adding duplicates, we make our result a set, then add tuples to the set. We do tuples here since lists are not hashable and cant be added to the set. At the end, we convert it back to lists and return.

#### Code
```python
        res = set()
        nums.sort()
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                for k in range(j + 1, len(nums)):
                    if (nums[i] + nums[j] + nums[k]) == 0:

                        res.add(tuple([nums[i], nums[j], nums[k]]))
        return [list(i) for i in res]
```

Time Complexity: $O(n^3))$
Space Complexity: $O(n^2)$

### Two Pointer Approach
we can sort the list, iterate the list. At each number, we use a two pointer method of the rest of the array to find its complement. This will allow us to reduce the time complexity.

#### Code
```python
        nums.sort()
        res = set()
        for i in range(len(nums) - 2):
            target = -1 * nums[i]
            low, high = i + 1, len(nums) - 1
            while (low < high):
                curr_sum = nums[low] + nums[high]
                if (curr_sum == target):
                    res.add(tuple([nums[i], nums[low], nums[high]]))
                    low += 1
                    high -= 1
                elif (curr_sum < target):
                    low += 1
                else:
                    high -= 1
        return [list(i) for i in res]
```

Time Complexity: $O(n^2)$
Space Complexity: $O(m)$, where $m$ is the number of result pairs. Worst case is $O(n^2)$.
