## Question
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 (sender) has the function:

```text
string encode(vector<string> strs) {
    // ... your code
    return encoded_string;
}
```

Machine 2 (receiver) has the function:

```text
vector<string> decode(string s) {
    //... your code
    return strs;
}
```

So Machine 1 does:

```text
string encoded_string = encode(strs);
```

and Machine 2 does:

```text
vector<string> strs2 = decode(encoded_string);
```

`strs2` in Machine 2 should be the same as `strs` in Machine 1.

Implement the `encode` and `decode` methods.

**Example 1:**

```java
Input: dummy_input = ["Hello","World"]

Output: ["Hello","World"]

Explanation:
Machine 1:
Codec encoder = new Codec();
String msg = encoder.encode(strs);
Machine 1 ---msg---> Machine 2

Machine 2:
Codec decoder = new Codec();
String[] strs = decoder.decode(msg);
```

**Example 2:**

```java
Input: dummy_input = [""]

Output: [""]
```

## Solution

### Using the Length of the string
We can attach the length of the string followed by a non-numerical character like `#`. Thus, each encoded string part will look like `length#string`.
#### Code
```python
def encode(self, strs: List[str]) -> str:
	res = ''
	for string in strs:
		length = len(string)
		res += str(length) + '#' + string
	return res

def decode(self, s: str) -> List[str]:
	res = []
	i = 0
	while i < len(s):
		j = i
		while s[j] != '#':
			j += 1
		length = s[i, j]
		j += 1
		res.append(s[j, j+length])
		i = j + length
	
	return res
```