## Question

A tandem bicycle is ridden by two individuals at a time. The max speed of the bicycle is the max speed of the two riders.

Given an array of two groups of riders. Find the optimal way to pair them to get the maximum speed and return the maximum speed.

Example

```python
Group1 = [4,5]
Group2 = [3,8]
```

The best pair is `(4,8), (5,3)` fielding a max speed of `8 + 5 = 13`

Source: AlgoExpert

## Solution

```python
class Solution:
    # The idea is to sort both lists and pair the max of group 1 with min of group 2.
    def max_speed(self,g1,g2):
        g1.sort() # -> nlogn
        g2.sort()  # -> nlogn
        max_speed = 0
        for i in range(len(g1)):
            speed  += g1[i] + g2[-i-1]
    return speed
```
