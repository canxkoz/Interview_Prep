## Question

## Solution

```python
    def expand(s, l,r):
        while l >= 0 and l < r:
            if s[l] == s[r]:
                l -= 1
                r += 1
            else:
                break
        return s[l+1:r]

    def find_palindrome(s):
        res = "
        for i in range(len(s)):
            odd = expand(s, i,i)
            even = expand(s, i,i+1)
            res = max(res, odd, even, key=len)
        return res
```
