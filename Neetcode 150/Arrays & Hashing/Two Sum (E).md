## Question
Given an array of integers `nums` and an integer `target`, return the indices `i` and `j` such that `nums[i] + nums[j] = target` and `i != j`.

We can assume that there always exists a single `[i, j]` solution pair. 

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
In this approach, we can use a HashMap to check for the complement ($nums[i] - target$) as we go through the array.

At each step in nums, we check if it is a complement of a number that came before it. If not, we add the index of the number, and its complement.

#### Code
```python
complement_map = {}
for i in range(len(nums)):
	if nums[i] in complement_map:
		return [complement_map[nums[i]], i]
	complement_map[target - nums[i]] = i
```

Time Complexity: O($n$)
Space Complexity: O($n$)