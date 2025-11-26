---
title: "Why Do We Square the Errors? Understanding Variance, SD, and MAD"
date: 2025-11-26
categories:
  - Statistics
  - Learning
tags:
  - math
  - data-science
  - feynman-technique
toc: true
toc_label: "Table of Contents"
toc_sticky: true
mathjax: true
header:
  teaser: https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80
---

When I first started diving into **AI and Data Science**, I treated statistics like a set of rules to memorize. I knew *how* to calculate Standard Deviation, but I didn't understand *why* the formula looked the way it did.

Why do we square the differences? Why not just take the absolute value?

This weekend, I took a step back to "derive" these concepts from scratch, using the Feynman Technique. Here is my log on the journey from the **Mean** to the **Standard Deviation**.

# 1. The Mean: The Center of Gravity

The mean is simple. It’s the balancing point of our data. If we have a dataset of my daily sleep hours: `[6, 7, 8, 9, 10]`, the mean is 8.

$$\mu = \frac{1}{N} \sum_{i=1}^{N} x_i$$

But the mean lies. Two datasets can have the same mean but look completely different.
* **Set A:** `[8, 8, 8, 8, 8]` (Mean: 8) -> Zero chaos.
* **Set B:** `[0, 0, 8, 16, 16]` (Mean: 8) -> Total chaos.

We need a way to measure the **"Chaos"** (Dispersion).

# 2. The Intuitive Approach: MAD (Mean Absolute Deviation)

My first thought was: *"If we want to know how far the data points are from the mean, why don't we just measure the distance?"*

If we just add the differences $(x_i - \mu)$, the negatives cancel out the positives, and we get zero. So, logically, we should take the **Absolute Value**.

$$MAD = \frac{1}{N} \sum_{i=1}^{N} |x_i - \mu|$$

This is called **Mean Absolute Deviation (MAD)**. It makes perfect sense. It’s intuitive.

**Why don't we use it everywhere?**
As I dug deeper into the math, I learned that MAD has a major flaw: **Calculus.** The absolute value function $|x|$ has a sharp corner at 0 (it's "V" shaped). You can't take the derivative at a sharp corner. This makes it a nightmare for optimization algorithms in AI (like Gradient Descent).

# 3. Variance: Penalizing the Outliers

Since we can't use absolute values easily, we need another way to get rid of negative signs. **We square them.**

This leads us to **Variance ($\sigma^2$)**.

$$\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2$$

### The "Aha!" Moment 💡
When I was playing with Python to visualize this, I realized something cool about squaring:
* If the error is **2**, the penalty is **4**.
* If the error is **10**, the penalty is **100**.

Squaring doesn't just make numbers positive; it **disproportionately punishes outliers**. In the world of statistics (and deep learning), being *very* wrong is much worse than being *slightly* wrong.

> **Note to self:** This is like my gym routine. Missing 1 day is okay (small deviation). Missing 10 days in a row is exponentially harder to recover from (huge variance).

# 4. Standard Deviation: Back to Reality

Variance is great, but it has a problem: The units are squared.
If I'm measuring my sleep in **hours**, the Variance is in **hours squared ($h^2$)**. What does "4 squared hours" even mean?

To fix this and get back to our original unit, we take the **Square Root**.

$$\sigma = \sqrt{\sigma^2} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2}$$

This is the **Standard Deviation ($\sigma$)**. It tells us, on average, how far a data point is from the mean, in understandable units.

# 5. Summary (TL;DR)

| Concept | Formula | Why use it? |
| :--- | :--- | :--- |
| **Mean** | $\mu$ | To find the center. |
| **MAD** | $\sum |x - \mu|$ | Intuitive, but hard to do calculus with. |
| **Variance** | $\sigma^2$ | Mathematically smooth, punishes outliers. |
| **Std. Dev** | $\sigma$ | Same as variance, but in readable units. |

### Code Snippet
Here is a quick Python function I wrote to compare them:

```python
import numpy as np

data = [6, 7, 8, 9, 10]

mean = np.mean(data)
mad = np.mean(np.abs(data - mean))
variance = np.var(data)
std_dev = np.std(data)

print(f"Mean: {mean}")
print(f"MAD: {mad}")
print(f"Variance: {variance}")
print(f"SD: {std_dev}")
