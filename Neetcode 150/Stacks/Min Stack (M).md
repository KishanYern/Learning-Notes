## Question
Design a stack class that supports the `push`, `pop`, `top`, and `getMin` operations.
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

Each function should run in O(1) time.

## Solution
### Two Stacks
Use one stack to keep track of the values of the stack (normal stack), and the other to keep track of the minimum element at that point in the stack. 

#### Code
```cpp
private:
    stack<int> stack1;
    stack<int> stack2;
  
public:

    MinStack() {

    }

    void push(int val) {
        stack1.push(val);
        int min_val = min(val, stack2.empty() ? val : stack2.top());
        stack2.push(min_val);
    }

    void pop() {
        stack1.pop();
        stack2.pop();
    }

    int top() {
        return stack1.top();
    }
    
    int getMin() {
        return stack2.top();
    }
```