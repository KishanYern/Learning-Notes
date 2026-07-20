## Question
There are `n` cars traveling to the same destination on a one-lane highway.

You are given two arrays of integers `position` and `speed`, both of length `n`.

- `position[i]` is the position of the `ith car` (in miles)
- `speed[i]` is the speed of the `ith` car (in miles per hour)

The **destination** is at position `target` miles.

A car can **not** pass another car ahead of it. It can only catch up to another car and then drive at the same speed as the car ahead of it.

A **car fleet** is a non-empty set of cars driving at the same position and same speed. A single car is also considered a car fleet.

If a car catches up to a car fleet the moment the fleet reaches the destination, then the car is considered to be part of the fleet.

Return the number of **different car fleets** that will arrive at the destination.

**Example 1:**

```java
Input: target = 10, position = [1,4], speed = [3,2]

Output: 1
```

Explanation: The cars starting at 1 (speed 3) and 4 (speed 2) become a fleet, meeting each other at 10, the destination.

**Example 2:**

```java
Input: target = 10, position = [4,1,0,7], speed = [2,2,1,1]

Output: 3
```

Explanation: The cars starting at 4 and 7 become a fleet at position 10. The cars starting at 1 and 0 never catch up to the car ahead of them. Thus, there are 3 car fleets that will arrive at the destination.

## Solution

### Using a Stack and calculating time

First we want to sort our lists with respect to their initial positions. Then for each of the cars, we want to calculate the expected times they would reach the target in $remaining{ }distance / speed$ time periods. Iterate back from the right. If we see a time period that is less than our current time, then we know that it would combine them into a single fleet. 

#### Code
```python
        res = 0
        pos_speed = [(position[i], speed[i]) for i in range(len(position))]
        pos_speed.sort(key = lambda x: x[0])
        times = [(target - pos_speed[i][0]) / pos_speed[i][1] for i in range(len(position))]

        while (len(times)):
            time = times.pop()
            
            while (len(times) and (times[-1] <= time)):
                times.pop()

            res += 1

        return res
```

Time Complexity: $O(nlogn)$
Space Complexity: $O(n)$
