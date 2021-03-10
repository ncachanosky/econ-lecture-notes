---
# Title, summary, and page position.
linktitle: "Functional forms"
weight: 2

# Page metadata.
title: Functional forms
type: book  # Do not modify.
---



---

## Alternative functional linear forms

Remember that OLS requires that the model is linear **on the coefficients**. The relationship between $y$ and your regressors may not be linear, even of the regression is. Recall that what OLS needs is:

$$
f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K x_K + \varepsilon
$$

After you identify all the relevant regressors to be included in the model, you need to decide on the functional form (relationship) between the dependent variable and the regressors. Different functional forms have convenient economic interpretations as well.

Let's discuss first the most common functional forms, how to pick the correct one, and then work through a `STATA` misspecification example.

---

## Common functional forms

For simplicity in the following discussion, assume the model has only one variable

### Linear

The linear model: $y = \beta_0 + \beta_1 x + \varepsilon$

#### Marginal effect

This functional form assumes that the relationship between the regressor and the dependent variable is **constant**. In other words, the model assumes a constant **marginal effect** of the regressors on the dependent variable.

$$
\frac{\Delta y}{\Delta x} = \beta_1
$$

#### Elasticity

Because the marginal effect is constant, the elasticity between the regressor and the dependent variable is not. The value of the elasticity depends on the interaction between (1) the slope between $y$ and $x$ and (2) the "position in the line" $(s/y)$.

$$
\epsilon_{(y,x)} = \frac{\Delta y}{\Delta x} \frac{x}{y} = \beta_1 \frac{x}{y}
$$

### Double-Log or Log-Log

The double-log model: $ln(y) = \beta_0 + \beta_1 ln(x) + \varepsilon$

### Semi-Logs: Lin-Log and Log-Lin

### Polynomial

### Inverse

### Combining functional forms

### Summary

Table
Matrix notation form

---

## Choosing the right functional form

---

## Example