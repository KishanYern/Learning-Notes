
## Question
Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.

**Example 1:**

```java
Input: s = "racecar", t = "carrace"

Output: true
```

**Example 2:**

```java
Input: s = "jar", t = "jam"

Output: false
```

Basically, the exact same (and number of) characters should be present in both `s` and `t`. 

## Solutions

### Brute Force Sorting
If we sort both strings, they should be the exact same if they are anagrams.
#### Code
```python
if len(s) != len(t):
	return False
	
return sorted(s) == sorted(t)
```

Time Complexity: O($nlogn$)
Space Complexity: O($n$). 
Note: Sorting in python uses TimSort, which is a mix of merge sort and insertion sort. 

### Counting Chars in Both Strings
If we count the number of characters in each string using a HashMap, then compare both HashMaps at the end, they should be the same if they are anagrams.
#### Code
```python
if len(s) != len(t):
	return False
	
s_map = {}
for char_s in s:
	s_map[char_s] = s_map.get(char_s, 0) + 1
	
t_map = {}
for char_t in t:
	t_map[char_t] = t_map.get(char_t, 0) + 1
	
return s_map == t_map
```

#### Better Code with 1 for loop
```python
if len(s) != len(t):
	return False
	
s_map, t_map = {}, {}
for i in range(len(s)):
	s_map[s[i]] = s_map.get(s[i], 0) + 1
	t_map[t[i]] = t_map.get(t[i], 0) + 1
	
return s_map == t_map
```

Time Complexity: O($n$)
Space Complexity: O($n$)

### Counting using Arrays
Since the problem guarantees lowercase English letters, we can set a fixed array of length 26, then count each letter based on their ASCII value difference from `a`. For example, `ord(b)` - `ord(a)` = 1.

For s, we would add 1 to the index. For t, we would subtract 1. 

At the end, we would go through all the values in the array. If there are only 0's, then they are anagrams.

#### Code
```python
if len(s) != len(t):
	return False
	
count = [0] * 26
for i in range(len(s)):
	count[ord(s[i]) - ord('a')] += 1
	count[ord(t[i]) - ord('a')] -= 1
	
for val in count:
	if val != 0:
		return False
		
return True
```

Time Complexity: O($n$)
Space Complexity: O($1$). This is because the space we allocated is constant at 26 integer values.