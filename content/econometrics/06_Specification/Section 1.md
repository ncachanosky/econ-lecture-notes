---
# Title, summary, and page position.
linktitle: "Regressors"
weight: 1

# Page metadata.
title: Regressors
type: book  # Do not modify.
---



---

## Omitted variable bias

Remember, coefficients show the marginal the effect of their regressors assuming constant **only** the other regressors **included** in the model. Therefore, omitting a variable can produce some bias in the coefficients of the included regressors **if** there is some correlation between the included regressors and the omitted variables.

### Simple example

Consider the following example. There is a true model with two regressors, but your model only includes one of them:

1. True model: $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \varepsilon$
2. Your model: $y = \beta_0^* + \beta_1^* x_1 + \varepsilon ^*$

All non-included regressors fall into the error term. Therefore, the error term of **your** model includes the pure classical error plus any omitted variable: $\varepsilon^* = varepsilon + \beta_2 x_2$.

As long as the omitted regressors are **irrelevant**, their coefficients will be zero $(beta_2 = 0)$, and therefore it won't affect the error term of your model. However, if $\beta_2 \neq0$, then $E[\varepsilon^*] = \beta_2 x_2 \neq0$.

If $x_1$ and $x_2$ are correlated, then $x_1$ will be correlated with $\varepsilon^*$: $\rho(x_1, x_2) \neq 0 \rightarrow \rho(x_1, \varepsilon^*) \neq 0$.

### General case: Matrix algebra

Let $X$ and $\beta$ be the matrix and coefficient-vector of the included regressors (including the constant). Let $Z$ and $\gamma$ be the matrix and vector-coefficient of the omitted variables, and $\xi$ by the vector-bias of each $beta$ included in the model. Then:

$$
\begin{align}
\hat{\beta}^*    &= \beta + (X'X)^{-1} \varepsilon^* \\\\[10pt]
\hat{\beta}^*    &= \beta + (X'X)^{-1} (\varepsilon + Z\gamma) \\\\[10pt]
E[\hat{\beta}^*] &= E \left[ \beta + (X'X)^{-1} (\varepsilon + Z\gamma) \right] \\\\[10pt]
E[\hat{\beta}^*] &= \beta + E[(X'X)^{-1}Z\gamma] \\\\[10pt]
E[\hat{\beta}^*] &= \beta + \xi
\end{align}
$$

---

## Irrelevant variable inefficiency