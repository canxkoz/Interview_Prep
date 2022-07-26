## Question

Given a string s, return the longest palindromic substring in s.

## Solution

```python
    def expand(s, l,r):
        while l >= 0 and r < len(s):
            if s[l] == s[r]:
                l -= 1
                r += 1
            else:
                break
        return s[l+1:r]

    def find_palindrome(s):
        res = "
        for i in range(len(s)):
            odd_length = expand(s, i,i)
            even_length = expand(s, i,i+1)
            res = max(res, odd_length, even_length, key=len)
        return res
```
