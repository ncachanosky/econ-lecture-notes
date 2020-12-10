---
# Title, summary, and page position.
linktitle: "The Gauss-Markov Theorem"
weight: 4

# Page metadata.
title: The Gauss-Markov Theorem
type: book  # Do not modify.
---



---

## The Gauss-Markov Theorem

The [Gauss-Markov Theorem](https://en.wikipedia.org/wiki/Gauss%E2%80%93Markov_theorem#Remarks_on_the_proof) proves important conditions of the OLS coefficient estimation. The exact nature of these conditions depend on whether **assumptions 1 to 6** or **assumptions 1 to 7** are met.

### BLUE coefficients.

**If assumptions 1 to 6** hold (everything except the normal distribution of the errors), then the estimated $betas$ are the **B**est **L**inear **U**nbiased **E**estimator (BLUE).

They key word in BLUE is *best*, which means that the variance of the estimated $betas$ is the minimum possible. Any estimation method other than OLS will produce $betas$ with a larger variance. The smaller the variance, the more likely the **estimated** $betas$ will be closer to the **true** $betas$.
