## Question
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements within the array. 
The test cases are generated such that the answer is always unique.
You may return the output in any order.

**Example 1:**

```java
Input: nums = [1,2,2,3,3,3], k = 2

Output: [2,3]
```

**Example 2:**

```java
Input: nums = [7,7], k = 1

Output: [7]
```

## Solution
### Using a Max Heap
Since we want the most frequent elements, using a heap should be intuitive. We need to first count the occurrences of all numbers, then put a tuple of (# of occurrences, item) and make a **max heap** using the first element. We will use the `Counter` function from now on since we have already done a lot of manually counting.
#### Code
```python
count_of_items = Counter(nums)
heap = []
for item, freq in count_of_items.items():
	heapq.heappush(heap, [freq, item])
	if len(heap) > k:
		heapq.heappop(heap) #This is because we only care about the top k

res = []
for _ in range(k):
	res.append(heapq.heappop(heap)[1])
return res
```

Time Complexity: O($n*logk$)
Space Complexity: O($n + k$)

### Using Bucket Sort
We count the elements like before. This time instead of using a heap, we use an 2d array of length `nums`. We place items in the array, their index being their freq. We then iterate backwards through the array until we have k elements.

#### Code
```python
count_of_items = Counter(nums) 
count_array = [] * len(nums)
for item, freq in count_of_items.items():
	count_array[freq].push(item)

res = []
for i in range(len(count_array) - 1, 0, -1):
	for num in count_array[i]:
		res.append(num)
		if len(res) == k:
			return res
```

Time Complexity: O($n$)
Space Complexity: O($n$)