---
layout: post
title: Largest Palindrome Problem
subtitle: 
---
#Step 1 - Understanding the problem
Here is the original problem: A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009.
Find the largest palindrome made from the product of two 3-digit numbers.

My first instinct was multiplying all three digit numbers and checking for palindrome ones. Yet after thinking some time i found a rule for palindromes. 
Every palindrome number must have eleven as a multipler. So i narrow down the numbers i will try to 3-digit multiples of eleven and another three digit number starting from 999.

#Step 2 - Coding
First i wrote the check algorithm. Since the biggest outcome must be 6-digit number, i didnt write it flexible. Yet, it can be flexible for checking any palindrome numbers with some small changes.
Anyways, in check function; we are looking for an unmatch in digits. If not, it returns the number. 
In finder function, we are multiplying every 3-digit number with ever 3-digit multipler of eleven. When function exits the while loop, it returns the biggest palindrome in the list.


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
    palindromes = []
    while multipler >= 110:
        palindromes.append(check(multipler*num))
        if num > 99:
            num -=1
        else:
            num = 999
            multipler -= 11
    return max(palindromes)
print(finder())
```
