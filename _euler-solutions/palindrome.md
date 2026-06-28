---
layout: post
title: "Largest Polindrome of three digit numbers of two"
subtitle: "My Python solution for the Palindrome Project Euler challenge"
---

### Problem Description
Find the largest palindrome made from the product of two 3-digit numbers.

### Solution Code
```python
def check(n):
    nums = [int(d) for d in str(n)]
    length = len(nums)
    if length < 6:
        return 0
    for i in range(0,int(round(length/2))):
        if nums[i] != nums[5-i]:
            return 0
    return n
def finder():
    multipler = 990
    num = 999
    list = []
    while multipler >= 110:
        list.append(check(multipler*num))
        if num > 99:
            num -=1
        else:
            num = 999
            multipler -= 11
    return max(list)
print(finder())
