---
layout: post
title: "Largest Polindrome of three digit numbers of two"
subtitle: "My Python solution for the first Project Euler challenge"
---

### Problem Description
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23. Find the sum of all the multiples of 3 or 5 below 1000.

### Solution Code
```python
def solve_problem_1():
    total_sum = sum(x for x in range(1000) if x % 3 == 0 or x % 5 == 0)
    return total_sum

print(solve_problem_1())
