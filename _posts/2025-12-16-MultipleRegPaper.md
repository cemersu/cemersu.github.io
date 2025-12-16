---
title: "Mastering Gradient Descent: The Art of Feature vs. Target Scaling"
date: 2025-12-11
categories:
  - Machine Learning
  - Experiments
tags:
  - python
  - linear-regression
  - gradient-descent
  - from-scratch
  - math
toc: true
toc_label: "Experiment Log"
toc_sticky: true
header:
  teaser: /assets/images/mlr-scaling/cover.png
---

Welcome back to the lab. 🧪

[cite_start]Gradient Descent is the backbone of modern machine learning optimization[cite: 13]. [cite_start]However, as I discovered in this latest experiment, its performance is incredibly sensitive to the scale of your data[cite: 14].

In my previous projects, I relied on libraries to handle the heavy lifting. [cite_start]This time, I built a **Multiple Linear Regression (MLR)** model from scratch using batch Gradient Descent to answer a specific question: **Should we scale just the inputs, or the targets as well?**[cite: 7, 8].

Here is my log of the experiment.

## 1. The Engine: Building the Regressor

Before running the tests, I implemented the math manually. The prediction function $\hat{y}$ for a given input vector is defined as:

$$
\hat{y} = w_{1}x_{1} + w_{2}x_{2} + ... + w_{n}x_{n} + b
[cite_start]$$ [cite: 22]

To train this, I used the **Mean Squared Error (MSE)** cost function. [cite_start]It’s perfect for Gradient Descent because it is convex and differentiable, meaning we can easily find the bottom of the "error valley"[cite: 31].

$$
J(w,b) = \frac{1}{n}\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}
[cite_start]$$ [cite: 29]

The weights were updated iteratively using the gradients:

$$
w_{j} := w_{j} - \alpha\frac{1}{n}\sum_{i=1}^{n}(\hat{y}_{i}-y_{i})x_{ij}
[cite_start]$$ [cite: 36]

## 2. The Setup

[cite_start]I used a student performance dataset ($n=10,000$)[cite: 8]. [cite_start]To evaluate the results fairly, I looked at the MSE for the loss, but I also calculated the **Mean Absolute Percentage Error (MAPE)** to get a percentage-based accuracy score[cite: 38].

I ran three distinct experiments to see how scaling affected convergence.

## 3. Experiment I: The "Hybrid" Approach (Winner) 🏆

**Configuration:**
* **Inputs (X):** Normalized to a standard range.
* [cite_start]**Targets (y):** Left in their natural scale (0-100 exam scores)[cite: 45].

**The Result:**
This configuration was the clear winner. [cite_start]The model converged within 2,000 epochs with a **MAPE of 3.73%**[cite: 47].

[cite_start]As you can see in the plot below, the predictions (blue dots) tightly follow the ideal red diagonal line, proving the model learned the distribution perfectly[cite: 48].

![Experiment 1 Results](/assets/images/mlr-scaling/ex1-results.png)
[cite_start]*(Figure 1: High accuracy fit with $R^2 \approx 0.99$) [cite: 64]*

## 4. Experiment II: The "Raw Data" Chaos

**Configuration:**
* **Inputs (X):** Unnormalized (Raw).
* [cite_start]**Targets (y):** Unnormalized (Raw)[cite: 65, 66].

**The Result:**
This was a disaster. The unnormalized inputs created an elongated loss landscape. [cite_start]When I used a standard learning rate ($\alpha=0.01$), I hit an `Overflow` error—**Exploding Gradients**[cite: 67].

[cite_start]I had to reduce the learning rate to a tiny $0.0001$ just to get it to run, and even then, the performance degraded significantly (MAPE 11.52%)[cite: 68]. [cite_start]The scatter plot showed much higher variance (noise) compared to Experiment I[cite: 69].

![Experiment 2 Results](/assets/images/mlr-scaling/ex2-results.png)

## 5. Experiment III: The "Over-Normalization" Trap

**Configuration:**
* **Inputs (X):** Normalized [0, 1].
* [cite_start]**Targets (y):** Normalized [0, 1][cite: 88].

**The Result:**
This was the most surprising finding. [cite_start]I assumed scaling everything would be better, but the model stopped learning entirely[cite: 89].

This led to the **Vanishing Gradient** problem. Because the target values were so small (< 1), the calculated gradients approached zero. [cite_start]The weights didn't update significantly, and the model got stuck predicting the **mean** of the dataset for every single student[cite: 91, 92].

![Experiment 3 Results](/assets/images/mlr-scaling/ex3-results.png)
[cite_start]*(Figure 3: The "Flatline." The model fails to learn the slope entirely.) [cite: 113]*

## Conclusion

[cite_start]This experiment provided empirical evidence of an asymmetry in Gradient Descent[cite: 116].

1.  [cite_start]**Scale your inputs:** It is non-negotiable for numerical stability and preventing exploding gradients[cite: 117].
2.  [cite_start]**Don't scale your targets (usually):** For regression tasks with bounded outputs, scaling targets to [0, 1] can compress gradients too much, trapping the model[cite: 121, 122].

The optimal configuration is a hybrid one: **Normalized Inputs + Natural Scale Targets**. [cite_start]This achieved the best balance of stability and precision (3.73% error)[cite: 124].

Next time, I'll be looking into how different weight initialization strategies might help solve some of these issues from the start!
