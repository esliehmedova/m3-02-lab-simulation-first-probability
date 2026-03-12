![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Simulation-First Probability

## Overview

Probability can feel abstract when you only see it through formulas and axioms. In this lab, you'll flip that approach: instead of calculating probabilities on paper first, you'll **simulate** random experiments in Python and let the numbers emerge from code. This "simulation-first" mindset is one of the most practical tools in a data scientist's toolkit — it lets you estimate probabilities for complex scenarios where closed-form solutions are hard to derive or don't exist at all.

You'll start with a classic Monte Carlo estimation (approximating π), then move through coin-flip experiments, binomial trials, and conditional probability. At each stage, you'll compare your simulation results against known theoretical values and watch how estimates converge as the number of trials grows. By the end, you'll have first-hand evidence that randomness is predictable in the aggregate — the foundation of statistical thinking.

This lab connects to the lesson on probability fundamentals. Where the lesson introduced concepts like sample spaces, independence, and conditional probability through definitions, here you'll verify those ideas by running thousands of experiments and plotting the results.

## Learning Goals

By the end of this lab, you should be able to:

- Estimate π using a geometric Monte Carlo method and explain why the estimate improves with more samples.
- Simulate Bernoulli and binomial experiments using `numpy.random`.
- Compute empirical probabilities from simulation output and compare them to theoretical values.
- Implement a conditional probability scenario via filtering simulation results.
- Visualize the Law of Large Numbers by plotting running estimates against sample size.
- Articulate when simulation is preferable to analytical calculation.

## Setup and Context

All work happens in a single Jupyter Notebook. You'll generate random data, run experiments, and visualize results — no external datasets are needed. The focus is on building and running simulations from scratch, so resist the urge to look up formulas first. Simulate, observe, then verify.

## Requirements

### Fork and clone

1. Fork this repository to your own GitHub account.
2. Clone the fork to your local machine.
3. Navigate into the project directory.

### Python environment

```bash
pip install pandas numpy matplotlib seaborn
```

- **Python** ≥ 3.9
- **numpy** — random number generation and array operations
- **matplotlib** — plotting convergence curves and distributions
- **seaborn** — statistical visualization
- **pandas** — optional, for organizing simulation results into tables

## Getting Started

1. Create a new Jupyter Notebook called **`m3-02-simulation-first-probability.ipynb`**.
2. Import cell:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

np.random.seed(42)
sns.set_style("whitegrid")
```

3. Work through the tasks sequentially. Each builds understanding for the next.
4. Write markdown cells between tasks to record your observations and reasoning.

## Tasks

### Task 1: Estimate π with Monte Carlo

The idea is simple: inscribe a circle of radius 1 inside a 2×2 square. If you throw random darts uniformly at the square, the fraction that land inside the circle should approximate π/4.

1. Generate **N = 100,000** random (x, y) points where x and y are each drawn from Uniform(−1, 1).
2. Classify each point as "inside" (x² + y² ≤ 1) or "outside" the unit circle.
3. Estimate π as `4 × (points inside) / N`.
4. Print your estimate alongside the true value of π.
5. Create a scatter plot of the first **5,000** points, coloring inside points differently from outside points. Draw the unit circle on top for reference.

**Convergence plot:** Compute the running estimate of π after every 100 points (i.e., at n = 100, 200, 300, …, 100,000). Plot this running estimate with a horizontal line at the true π. Add a title and axis labels.

**Guiding question:** At roughly what sample size does your estimate stabilize within ±0.01 of true π?

### Task 2: Coin Flips and Empirical Probability

Simulate a series of fair coin flips and observe how the empirical probability of heads converges to 0.5.

1. Simulate **10,000** fair coin flips (use `np.random.choice([0, 1])` or `np.random.binomial(1, 0.5, size=10000)`).
2. Compute the running proportion of heads after each flip (cumulative sum divided by cumulative count).
3. Plot the running proportion with a horizontal line at 0.5. Use a log-scaled x-axis so you can see early fluctuations and later stabilization clearly.
4. Repeat the experiment **5 times** (5 independent series of 10,000 flips) and overlay all 5 convergence paths on the same plot with different colors.

**Guiding question:** How many flips does it typically take for the running proportion to stay within ±0.01 of 0.5?

### Task 3: Simulating Binomial Experiments

A factory produces widgets with a 3% defect rate. A quality inspector samples 50 widgets per batch.

1. Simulate **10,000 batches** of 50 widgets each, where each widget has a 3% chance of being defective.
2. For each batch, record the number of defective widgets found.
3. Plot a histogram of the defect counts across all 10,000 batches. Overlay the theoretical Binomial(n=50, p=0.03) PMF as points connected by a line.
4. From your simulation, estimate:
   - P(0 defects in a batch)
   - P(3 or more defects in a batch)
   - The expected number of defects per batch
5. Compare each simulation estimate to the theoretical binomial value (use `scipy.stats.binom` or manual calculation).

**Guiding question:** How close are your empirical estimates to the theoretical values? Would 1,000 batches have been enough, or do you need 10,000?

## Submission

### What to submit

- `m3-02-simulation-first-probability.ipynb` — your completed notebook with all code, outputs, and markdown explanations.

### Definition of done (checklist)

- [ ] All three tasks are completed with code and visible outputs.
- [ ] Monte Carlo π estimate is within ±0.02 of true π (with 100,000 samples).
- [ ] Convergence plots clearly show stabilization over increasing sample sizes.
- [ ] Binomial simulation results are compared to theoretical values.
- [ ] The notebook runs top-to-bottom without errors (`Kernel → Restart & Run All`).

### How to submit (Git workflow)

```bash
git add .
git commit -m "lab: complete simulation-first probability"
git push origin main
```

Then open a **Pull Request** on the original repository with a brief description of your work.
