---
title: "Reinventing the Wheel: Building a Polynomial Engine from Scratch"
date: 2025-12-03
categories:
  - Programming
  - Mathematics
tags:
  - python
  - oop
  - calculus
  - algorithms
toc: true
toc_label: "Lab Notes"
toc_sticky: true
header:
  teaser: /assets/images/polynomial-project/polynomial-cover.jpg
---

Welcome to the lab. 🧪

In the world of data science, we often take libraries like NumPy or SciPy for granted. We call a function, and the math happens inside a "black box." But following the Feynman technique, I believe you don't truly understand a concept until you can build it yourself.

Today, I decided to deconstruct high-school algebra and calculus and reconstruct them using Python's Object-Oriented Programming (OOP). The result is **`ErsuPolynomials`**, a custom class that handles polynomial arithmetic and calculus logic without external dependencies.

## 1. The Philosophy: Code as Math

The goal was not just to store numbers, but to create an object that behaves like a mathematical entity.
* It should print like a math equation ($3x^2 - 5$), not a Python list (`[3, 0, -5]`).
* It should allow direct interaction using standard operators (`+`, `*`).
* It should be able to differentiate itself (Calculus).

## 2. The Aesthetics: Making it Human-Readable

The hardest part wasn't the integration logic; it was the string formatting (`__str__`).

A raw list like `[1, -1, 0, 5]` implies $x^3 - x^2 + 5$. However, writing a logic tree to handle this gracefully was a challenge. I had to handle:
* **Superscripts:** Rendering `x^power`.
* **The "One" Problem:** Suppressing coefficients of `1` and `-1` (writing `x` instead of `1x`).
* **Sparsity:** Skipping terms with `0` coefficients completely.
* **Signs:** Managing the `+ -` concatenation issues.

## 3. The Logic: Multiplication & Calculus

### The Multiplication Challenge
Adding polynomials is simple linear alignment. Multiplying them is a combinatorial problem.
$$(ax + b)(cx + d) = acx^2 + adx + bcx + bd$$

To solve this efficienty, I avoided nested lists and used a **Dictionary (Hash Map)** approach:
1.  Iterate through both coefficient lists.
2.  Calculate `new_power = p1 + p2` and `new_coef = c1 * c2`.
3.  Store them in a dictionary to sum up overlapping powers automatically.
4.  Convert back to a list structure, filling gaps with zeros.

### The "Aliasing" Trap in Derivatives
While implementing the `derivative()` method, I fell into a classic Python trap: **Mutability.**

Initially, my code was modifying the original polynomial because `list = self.list` only copies the reference, not the data. I fixed this by implementing `self.coef.copy()`, ensuring that taking a derivative creates a *new* object without mutating the parent.

## 4. The Source Code

Here is the final, working implementation of the `ErsuPolynomials` class:

<script src="https://gist.github.com/cemersu/2962f527cfb5148e0adb38a66532fcc6.js"></script>

Conclusion
Building this from scratch gave me a deeper appreciation for the tools we use daily. It’s one thing to know the power rule; it’s another to teach it to a computer.

ErsuLabs — Deconstructing complexity, stay tuned.
