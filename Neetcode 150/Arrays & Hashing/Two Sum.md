## Question
Given an array of integers `nums` and an integer `target`, return the indices `i` and `j` such that `nums[i] + nums[j] = target` and `i != j`.

We can assume that there always exists a `[i, j]` pair. 

**Example 1:**

```java
Input: 
nums = [3,4,5,6], target = 7

Output: [0,1]
```

Explanation: `nums[0] + nums[1] == 7`, so we return `[0, 1]`.

**Example 2:**

```java
Input: nums = [4,5,6], target = 10

Output: [0,2]
```

**Example 3:**

```java
Input: nums = [5,5], target = 10

Output: [0,1]
```

### Solutions

### Brute Force (Double For Loop)
We can loop through every possible combination of the items in num, and see if their sum is equal to target. 
#### Code
```python
for i in range(len(nums)):
	for j in range(i + 1, len(nums)):
		if nums[i] + nums[j] == target:
			return [i, j]
```

Time Complexity: O($n^2$)
Space Complexity: O(1)

### Storing and Checking Against Complement
In this approach, we can use a HashMap 