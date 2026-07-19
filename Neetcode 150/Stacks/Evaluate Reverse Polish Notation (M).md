You are given an array of strings `tokens` that represents a **valid** arithmetic expression in [Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation).

Return the integer that represents the evaluation of the expression.

- The operands may be integers or the results of other operations.
- The operators include `'+'`, `'-'`, `'*'`, and `'/'`.
- Assume that division between integers always truncates toward zero.

**Example 1:**

```java
Input: tokens = ["1","2","+","3","*","4","-"]

Output: 5

Explanation: ((1 + 2) * 3) - 4 = 5
```

## Solution

### Using a stack
Same as we did in class. Biggest thing is to pop in reverse order to ensure that subtraction and division dont get messed up.

#### Code
```python
        stack = []
        for token in tokens:
            # If we get an operator
            if token == '+':
                num2 = stack.pop()
                num1 = stack.pop()
                new_num = num1 + num2

            elif token == '-':
                num2 = stack.pop()
                num1 = stack.pop()
                new_num = num1 - num2

            elif token == '*':
                num2 = stack.pop()
                num1 = stack.pop()
                new_num = num1 * num2

            elif token == '/':
                num2 = stack.pop()
                num1 = stack.pop()
                new_num = int(num1 / num2)

            else:
                # If we get an operand
                new_num = int(token)

            stack.append(new_num)

        return stack.pop()
```