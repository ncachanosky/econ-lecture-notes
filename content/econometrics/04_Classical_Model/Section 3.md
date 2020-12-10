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

### Efficiency