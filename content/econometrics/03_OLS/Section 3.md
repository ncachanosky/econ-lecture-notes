---
# Title, summary, and page position.
linktitle: "Evaluating the quality of a regression"
weight: 3

# Page metadata.
title: Evaluating the quality of a regression
type: book  # Do not modify.
---



---

## Methods to evaluate the quality of a regression

To evaluate how good an econometric model represents and matches the observed data requires considering several different issues. The proper evaluation of an econometric model requires an holistic approach. As is usual in econometrics, there are objective (numbers) and subjective (interpretation) issues at stake.

For instance, an econometric model of good quality should check the following boxes:

- [x] Does the model reflect sound economic theory?
- [x] Does the model include all the important regressors?
- [x] Are the estimated coefficients reasonable? Do their values contradict any economic theory or intuition?
- [x] Is the regression free of econometric problems? (later chapters)
- [x] How close to real data does are the model estimations? (this chapter)

This chapter deals with the last question. Namely, how good the *fit* of the model is. There are different ways to measure the goodness of fit of the model. First, we will go through the **coefficients of determination**. Second, we will go through three common **information criteria** indicators.

## Coefficients of determination

### Partition of sum of squares

Before building a measure of goodness of fit we need to decompose the variance of $y$ (the dependent variable) **around its mean**. The decomposition has three components.

First, the deviation of the observed data from its mean. The second one is the deviations that the model can predict of the dependent variable from its mean. And the third one is the residual, the difference between the difference between observed data and its mean and predicted data and the observed mean.

Since we are looking at **[variances](https://en.wikipedia.org/wiki/Variance)**[^1], these three measures will squared and added. Therefore, we have (1) the total sum of squares (TTS), (2) the explained sum of squares (ESS), and (3) the residual sum of squares (ESS). Then, the partition of sum squares is:

$$
\begin{align}
\overbrace{\sum_i (y_i - \bar{y})^2}^{\text{TSS}} &= \overbrace{\sum_i (\hat{y}_i - \bar{y})^2}^{\text{ESS}} + \overbrace{\sum_i (y_i - \hat{y}_i)^2}^{\text{RSS}} \\\\[10pt]
\sum_i (y_i - \bar{y})^2 &= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2
\end{align}
$$



### The $R^2$ (R-squared)

### The $\bar{R}^2$ (adjusted R-squared)

---

## Information criteria

### Maximum likelihood

### AIC: Akaike Information Criterion

### BIC: Bayesian Information Criterion

### HQC: Hannan-Quinn Information Criterion

---

## Appendix

### Proof: $TSS = ESS + RSS$

$$
\begin{align}
\sum_i (y_i - \bar{y})^2 &= \sum_i (y_i - \bar{y} + \hat{y}_i - \hat{y}_i)^2 \\\\
&= \sum_i \left( (\hat{y}_i - \bar{y}) + (y_i - \hat{y}_i) \right)^2 \\\\
&= \sum_i \left( (\hat{y}_i - \bar{y}) + e_i \right)^2 \\\\
\end{align}
$$




$$
\begin{align}
&= \sum_i \left( (\hat{y}_i - \bar{y}) + e_i \right)^2 \\\\
&= \sum_i \left( (\hat{y}_i - \bar{y})^2 + e_i^2 + 2 \sum_i (y_i - \bar{y}) e_i \right) \\\\
&= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2 + 2 \sum_i e_i (\hat{\beta}_0 + \hat{\beta}_1 x_{1,i} + ... + \hat{\beta}_K x_{K,i} - \bar{y}) \\\\
&= \sum_i (y_i - \hat{y})^2 + \sum_i e_i^2 + 2 (\hat{\beta}_0 - \bar{y}) \overbrace{\sum_i e_i}^{0} + 2 \hat{\beta}_1 \overbrace{\sum_i e_i x_{1,i}}^{0} + ... + 2 \hat{\beta}_K \overbrace{\sum_i e_i x_{K,i}}^{0} \\\\
\sum_i (y_i - \bar{y})^2 &= \sum_i (y_i - \hat{y})^2 + \sum_i e_i^2 \\\\
TSS &= ESS + RSS
\end{align}
$$

<!-- FOOTNOTES -->
[^1]: Recall that the variance of a **random** variable $x$ is: $\sum_i = p_i (x_i - \bar{x})^2$ (where $0 < p_i< 1$). If all values of $x$ have the same probability and there are $n$ observations, then $p_i = \frac{1}{n}$.