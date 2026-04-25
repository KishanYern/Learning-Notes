## Question
Given an integer array `nums`, return an array `output` where `output[i]` is the product of all the elements of `nums` except `nums[i]`.
Each product is guaranteed to fit in a **32-bit** integer.
Follow-up: Could you solve it in O($n$) time without using the division operation?

**Example 1:**

```java
Input: nums = [1,2,4,6]

Output: [48,24,12,8]
```

**Example 2:**

```java
Input: nums = [-1,0,1,2,3]

Output: [0,-6,0,0,0]
```

## Solutions

### Brute Force (double for loop)
We for each number in `nums`, we can loop through and multiply every other number in `nums`.
#### Code
```python
res = []
for i in range(len(nums)):
	product = 1
	for j in range(len(nums)):
		if i == j:
			continue
		product *= nums[j]
	res.append(product)
	
return res
```

Time Complexity: O($n^2$)
Space Complexity: O($1$) extra space.
### Division
When dividing, we want to look out for zeros so we don't get a division-by-zero error. There are three cases depending on the number of zeros in the array:
1. Two or more zeros: If there are two or more zeros, then we know that the product at every product will be a zero. Consider a non-zero number in `nums`, the product will be zero as there exists a zero outside of our number. Consider a zero number in `nums`, there still exists a zero outside of this zero, making the product zero.
2. Exactly one zero: If there is only one zero, then that position will be the only product that is non-zero. All other products will contain this zero and will multiply to zero.
3. If there are no zeros: If there are no zeros, then we can safely just divide the main product by the number we are on.
#### Code
```python
product, num_zeros = 1, 0
for num in nums:
	if num == 0:
		num_zeros += 1
		continue
	product *= num

if num_zeros > 1:
	return [0 for _ in range(len(nums))]
	
res = [0] * len(nums)
for i, c in enumerate(nums):
	if num_zeros: res[i] = 0 if c else product
	else: res[i] = product // c

return res
```
Time Complexity: O($n$)
Space Complexity: O($1$) extra space.
### Prefix and Postfix Product using arrays
For `output[i]`, we would need to multiply all the elements to the left of `i`, with all the elements to the right of `i`. If we can track the prefix and postfix products for all the elements, we can find our output by multiplying them together: `output[i] = prefix[i] * postfix[i]`.
#### Code
```python
n = len(nums)
prefix_array = [0] * n
prefix_array[0] = 1
for i in range(1, len(nums)):
	prefix_array[i] = prefix_array[i-1] * nums[i-1]

postfix_array = [0] * n
postfix_array[n - 1] = 1
for i in range(len(nums) - 2, -1, -1):
	postfix_array[i] = postfix_array[i+1] * nums[i+1]
	
return [prefix_array[i] * postfix_array[i] for i in range(n)]
```
Time Complexity: O($n$)
Space Complexity: O($n$) extra space.
### Prefix and Postfix Product without using arrays
We don't really need to store the prefix and postfix in its own arrays. We can store them in the result array, and storing the continuous prefix/postfix product in its own variable. 
#### Code
```python
n = len(nums)
res = [0] * n
res[0] = 1

prefix = 1
for i in range(1, n):
	prefix *= nums[i-1]
	res[i] = prefix
	
postfix = 1
for i in range(n-2, -1, -1):
	postfix *= nums[i+1]
	res[i] *= postfix
	
return res
```
Time Complexity: O($n$)
Space Complexity: O($1$) extra space.