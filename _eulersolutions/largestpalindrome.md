---
layout: post
title: Largest Palindrome Problem
subtitle: My python solution
---

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
