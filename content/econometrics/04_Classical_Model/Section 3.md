---
# Title, summary, and page position.
linktitle: "The Sample Distribution of the betas"
weight: 3

# Page metadata.
title: The Sample Distribution of $\hat{\beta}$
type: book  # Do not modify.
---



---

## Coefficients estimation and sample distribution

Recall that a regression **estimates** a value of an unobserved/unknown **true** $beta$. That $\hat{\beta}$ is an estimated value it means that it has a probability distribution. 

Every different sample taken from the total population will produce different values of $\hat{\beta}$. From all the potential different samples you can get, you get to work with only one. That is, from all the potential different values of $\hat{\beta}$ you can calculated, you only get to observe one.

A good sample and a good estimation technique will increase the likelihood that $\hat{\beta}$ will be close to $\beta$. To understand how this works, we need to have a closer look at the OLS coefficient estimation.

Recall that, in matrix notation:

$$
\begin{aligned}
y =& X\beta + \varepsilon \\\\[10pt]
\hat{\beta} =& \left( X'X \right) ^{-1} X'y
\end{aligned}
$$

Use now the first equation into the second one (where $I$ is the identity matrix):

$$
\begin{aligned}
\hat{\beta} =& \left( X'X \right)^{-1} \left(X'X \right) \beta + \left(X'X \right)^{-1} X \varepsilon \\\\[10pt]
\hat{\beta} =& I \beta + \left(X'X \right)^{-1} X \varepsilon
\end{aligned}
$$

You can see that because $\varepsilon$ is a random variable, so is each $\hat{\beta}$. Therefore, $\hat{\beta}$ has a mean and a standard deviation, which are related to the concept of unbiased and efficient estimation respectively.

---

## Unbiasedness and Efficiency

### Unbiasedness

An estimation is unbiased if its expected value coincides with the true value under estimation. A biased estimation would be the opposite, when the expected value of the estimation diverges from the true value under estimation. 

Consider the following example. The bullseye of a target is the true value. The darts you through are your estimations. If your darts miss but fall around the target, your estimations are unbiased. If you average all your estimations you get the true value. If, however, your darts fall in average to the side of the target, then your estimation is biased. You tend to err more to one side in such that if you average all your estimations you do not get the true value under estimation. In addition, how far away from each other each dart is represents the standard deviation of your estimation technique.

We can represent an unbiased and biased estimation the following way:

1. Unbiased estimation: $E[\hat{\beta}] = \beta$
2. Biased estimation: $E[\hat{\beta}] = \beta + \xi, \; \xi \neq 0$

You already know that your estimation will not be perfect. But, you **do not want** your estimation to be biased.

If assumptions 1 to 6 of the classical model hold, then OLS produces unbiased estimators.

$$
\begin{aligned}
\hat{\beta} =& \beta + \left(X'X \right)^{-1} X' \varepsilon \\\\[10pt]
E[\hat{\beta}] =& E \left[ \beta + \left(X'X \right)^{-1} X' \varepsilon \right] \\\\[10pt]
E[\hat{\beta}] =& \beta + \left(X'X \right)^{-1} X' E[\varepsilon] \\\\[10pt]
E[\hat{\beta}] =& \beta
\end{aligned}
$$

If *assumption 2** does not hold, then $E[\varepsilon] \neq 0$ and therefore $E[\hat{\beta}] \neq 0$. Recall that a reason why $E[\varepsilon] \neq 0$ is omitting a significant variable $(Z)$:

$$
\begin{aligned}
\varepsilon =& \varepsilon^* + \gamma Z \\\\[10pt]
E[\varepsilon] =& E\left[ \varepsilon^* + \gamma Z \right] \\\\[10pt]
E[\varepsilon] =& E[\varepsilon^*] + E[\gamma Z] \\\\[10pt]
E[\varepsilon] =& \gamma Z \neq 0
\end{aligned}
$$

### Efficiency