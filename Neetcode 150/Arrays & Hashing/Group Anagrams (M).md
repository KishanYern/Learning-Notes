## Question
Given an array of strings `strs`, group all anagrams together into sublists. You may return the output in **any order**. 

An **anagram** is a string that contains the exact same character as another string, but the order of the characters can be different. 

**Example 1:**

```java
Input: strs = ["act","pots","tops","cat","stop","hat"]

Output: [["hat"],["act", "cat"],["stop", "pots", "tops"]]
```

**Example 2:**

```java
Input: strs = ["x"]

Output: [["x"]]
```

**Example 3:**

```java
Input: strs = [""]

Output: [[""]]
```


## Solutions

### Sorting
Since each sorted value of any anagram is the same, we can use it as a key for a HashMap.
#### Code
```python
anagrams = defaultdict(list)
for string in strs:
	anagrams[''.join(sorted(string))].append(string)
	
return list(anagrams.values())
```
**Note**: We use `''.join(sorted(string))` here because the `sorted()` function on a string returns a list of the characters of that string in sorted order.
Time Complexity: O($n * nlogn$)
Space Complexity: O($n * k$)

### Using a HashMap for the Counter Array.

We would use the same technique as in **Valid Anagram** to store the count of the characters for a string `s`. We would use this count array as the key for a hashmap, where the value is an array. `s` would be added to that array. At the end, return the values().
#### Code
```python
anagrams = defaultdict(list)
for string in strs:
	count_array = [0] * 26
	for ch in string:
		count_array[ord(ch) - ord('a')] += 1
	anagrams[count_array].append(string)

return list(anagrams.values())
```

Time Complexity: O($n * k$), where n is the number of strings in the array and k is the average length of a string in the array.
Space Complexity: O($n * k$)