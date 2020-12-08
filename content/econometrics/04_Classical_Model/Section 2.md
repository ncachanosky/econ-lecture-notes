---
# Title, summary, and page position.
linktitle: "The Classical Assumptions"
weight: 2

# Page metadata.
title: The Classical Assumptions
type: book  # Do not modify.
---



---

## Assumption 1: The model is linear

This assumption requires the model to be **linear** and, of course, be correctly specified (your linear models is a good reflection of the underlying data relationship). However, we need to careful with what we mean by **linear** in this context.

{{% callout note %}}
The term **linear** refers to the coefficients, not to the regressors.
{{% /callout %}}

The following is a typical linear model with an additive error term:

$$
y_i = \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i
$$

The expression **linear model** can be confusing. We tend to think in *math terms*, where lineal equation is one with **linear variables**, that is, elevated to the power 1: $y = a + b_1 x_1 + b_2 x_2 + b_3 x_3$.

However, the classical assumption requires the model to be linear on the coefficients. As long as there are independent additive terms with linear coefficients, then the model is linear. Remember that what we are estimating is the $betas$, no the regressors.

Consider first a linear model with non-linear regressors. Let the first model have $w_i^2$ regressors and the second model have $ln(w_i)$ regressors. In both cases, regressors are no linear. These two examples are easy to linearize, just define $x_i = w_i^2$ in the first model and $x_i = ln(w_i)$ in the second model. Then:

$$
\begin{align}
y_i =& \beta_0 + \beta_1 \underbrace{z_i^2}_{x_1} + ... + \beta_k \underbrace{x_K^2}_{x_K} + \varepsilon_i \\\\[10pt]
y_i =& \beta_0 + \beta_1 \underbrace{ln(z_1)}_{x_1} + ... + \beta_k \underbrace{ln(z_K)}_{x_k} + \varepsilon_i
\end{align}
$$

*Econometrically speaking*, both models are identical in the sense that both are linear and with the same number of regressors. Of course, since we are looking at different data the estimated $betas$ will differ. Yet, both models are identical in the sense of how they are represented and how the $betas$ are estimated.

Consider now a non-linear theory that can be linearized before running your regression. For instance, your theory may be represented by the following equation:

$$
y = e^{\beta_0} x_1^{\beta_1} ... x_k^{\beta_k} e^{\varepsilon}
$$

You can easily linearize this model by applying logs (where $y^* = ln(y)$):

$$
\begin{align}
ln(y_i) =& \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i \\\\[10pt]
y^*_i =& \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i
\end{align}
$$

In general terms, a linear in the coefficients model has the following functional form: $f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K f(x_K)$.

An example of a model non-linear in the coefficients would be $y = \beta_0 + x_1^{\beta_1} + ... + x_k^{\beta_K}$. There is no arrangement that would make this equation linear on the $betas$.

There two other important conditions in this assumption:

1. The model is correctly specified, meaning there is no **omitted variables**
2. The error term is additive to the model and cannot be multiplied by or divided by any other regressor(s) included in the model

**Assumption 1** requires that your econometric model can be represented as a model linear *on the coefficients*, even if the regressors do not have a linear behavior or if the underlying theory is not linear.

---

## Assumption 2: The error term has zero population mean

---

## Assumption 3: All explanatory variables are uncorrelated with the error term

---

## Assumption 4: Observations of the error term are uncorrelated with each other

---

## Assumption 5: The error term has a constant variance (homoskedasticity)

---

## Assumption 6: No explanatory variable is a perfect linear combination of other(s) explanatory variable(s)

---

## Assumption 7: The error term is normally distributed

---

## Summary of the Classical Assumptions