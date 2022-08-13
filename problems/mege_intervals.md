## Question

Given an array of intervals where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Source: https://leetcode.com/problems/merge-intervals/

## Solution

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        start,end = intervals[0]
        res = []
        for interval in intervals[1:]:
            if interval[0] <= end:
                end = max(end, interval[1])
            else:
                res.append([start,end])
                start = interval[0]
                end = interval[1]
        res.append([start,end])
        return res
```
