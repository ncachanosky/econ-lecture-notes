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

All non-included regressors fall into the error term. Therefore, the error term of **your** model includes the pure classical error plus any omitted variable: $\varepsilon^* = \varepsilon + \beta_2 x_2$.

As long as the omitted regressors are **irrelevant**, their coefficients will be zero $(\beta_2 = 0)$, and therefore it won't affect the error term of your model. However, if $\beta_2 \neq0$, then $E[\varepsilon^\*] = \beta_2 x_2 \neq0$.

If $x_1$ and $x_2$ are correlated, then $x_1$ will be correlated with $\varepsilon^\*$: $\rho(x_1, x_2) \neq 0 \rightarrow \rho(x_1, \varepsilon^*) \neq 0$.

### General case: Matrix algebra

Let $X$ and $\beta$ be the matrix and coefficient-vector of the included regressors (including the constant). Let $Z$ and $\gamma$ be the matrix and vector-coefficient of the omitted variables, and $\xi$ by the vector-bias of each $beta$ included in the model. Then:

$$
\begin{align}
\hat{\beta}^*    &= \beta + (X'X)^{-1} X' \varepsilon^* \\\\[10pt]
\hat{\beta}^*    &= \beta + (X'X)^{-1} X' (\varepsilon + Z\gamma) \\\\[10pt]
E[\hat{\beta}^*] &= E \left[ \beta + (X'X)^{-1} X' (\varepsilon + Z\gamma) \right] \\\\[10pt]
E[\hat{\beta}^*] &= \beta + (X'X)^{-1} \underbrace{E[X'\varepsilon]}\_{\text{0}} + \underbrace{E[(X'X)^{-1} X'Z \gamma]}\_{\xi} \\\\[10pt]
E[\hat{\beta}^*] &= \beta + \underbrace{(X'X)^{-1} X'Z}\_{P_{X,Z}} \gamma \\\\[10pt]
E[\hat{\beta}^*] &= \beta + \xi; \qquad (\xi = P_{X,Z}\gamma)
\end{align}
$$

Unless $\gamma=0$ (irrelevant variables) or $(X'Z)=0$ ("uncorrelation" between the included and omitted regressors), $\hat{\beta}$ will be biased. The bias of each $beta$ depends on the coefficients of the omitted variables $(\gamma)$ and on the interaction between the included and omitted variables.

Each column in $P_{X,Z}$ includes the OLS slope between each included and excluded regressor: $X_i  = \alpha_0 + p_{i,j} Z_j + u$.

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/06_Specification/Omitted variable bias.xlsx" %}}Download Excel sample file.{{% /staticref %}}

---

## Irrelevant variable inefficiency
