## Question
Given an array nums, return true if any value appears more than once in the array, otherwise return false.

**Example 1:**

```java
Input: nums = [1, 2, 3, 3]

Output: true
```


**Example 2:**

```java
Input: nums = [1, 2, 3, 4]

Output: false
```

## Solutions

### Brute Force
Run a double for loop through pairs of elements, then compare each of them. If any are equal, return true. If we make it through the for loop and don't break out via the return, return false.

#### Code
```python
for i in range(len(nums)):
	for j in range(i + 1, len(nums)):
		if nums[i] == nums[j]:
			return True

return False
```

Time Complexity: O($n^2$)
Space Complexity: O(1)
### Set
Set up a `Set` to keep track of unique items in the array. We iterate through and add items into the set. If that item already exists in the set, return true. Else return false.

#### Code
```python
existing_nums = set()
for num in nums:
	if num in existing_nums:
		return True
	else:
		existing_nums.add(num)
return False
```

Time Complexity: O($n$)
Space Complexity: O($n$)

### Checking the length of array and set
For this method, we add the entire array into a set. If the length of that set is the same as the length of the array, then we know that the array consists of all unique elements. 

How? A set can not contain duplicate elements. If we add two of the same item into a set, the second item does not get added. Thus, if there is a duplicate element in the array, it wont count towards the length of the set. 

#### Code
```python
return not (len(set(nums)) == len(nums))
```

Time Complexity: O($n$)
Space Complexity: O($n$)