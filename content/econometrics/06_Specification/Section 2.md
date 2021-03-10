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

* If $x$ changes by 1 unit, $y$ changes $\beta$ times

This functional form assumes that the relationship between the regressor and the dependent variable is **constant**. In other words, the model assumes a constant **marginal effect** of the regressors on the dependent variable. Because the marginal effect is constant, the elasticity between the regressor and the dependent variable is **not constant**. The value of the elasticity depends on the interaction between (1) the slope between $y$ and $x$ and (2) the "position in the line" $(s/y)$.


$$
\begin{aligned}
\frac{\Delta y}{\Delta x} &= \beta_1 \\\\[10pt]
\epsilon_{(y,x)} &= \frac{\Delta y}{\Delta x} \frac{x}{y} = \beta_1 \frac{x}{y}
\end{aligned}
$$

### Double-Log or Log-Log

The log-log model: $ln(y) = \beta_0 + \beta_1 ln(x) + \varepsilon$

* If $x$ changes 1%, $y$ changes $\beta$%

The log-log-model has the convenient feature of producing a **constant** elasticity captured in the estimated coefficient. This functional form yields the opposite result than the linear model. Because the elasticity is constant, the marginal effect of $x$ on $y$ is **not constant**.

$$
\begin{aligned}
\frac{\Delta y}{\Delta x} &= \frac{y}{x} \bar{\epsilon}_{y,x} \\\\[10pt]
\epsilon_{y,x} =& \frac{\Delta y}{y} \frac{x}{\Delta x} = \frac{\Delta ln(y)}{\Delta ln(x)} = \beta_1
\end{aligned}
$$

### Semi-Logs: Lin-Log and Log-Lin

The lin-log model: $y = \beta_0 + \beta_1 ln(x) + \varepsilon$
The log-lin model: $ln(y) = \beta_0 + \beta_1 x + \varepsilon$

* Lin-log model: If $x$ changes 1%, $y$ changes $\beta$ times
* Log-lin model: If $x$ changes 1 unit, $y$ changes $\beta$%

The **lin-log** model assumes that the effect of $x$ on $y$ increases at a decreasing rate. This is a very common relationship in economics. For example, the productivity of hours of work, or the impact of income on consumption. 

The **log-lin** models assumes assumes that $y$ makes a percent adjustment to an absolute change in $x$. For instance, a change in the absolute profit of firm results in a percent change increase in wages.

### Polynomial

A polynomial function captures a non-constant slope that depends on the value of the regressor. Consider a second-degree polynomial (quadratic) form.

The quadratic model: $y = \beta_0 + \beta_1 x + \beta_1 x^2 + \varepsilon$

* If $x$ changes by 1 unit. $y$ changes $(\beta_1 + \beta_2 x)$ times

A quadratic function can be use to model a typical cost function, where $y$ is output, $\beta_0$ is the fixed cost, and the other two terms capture variable costs of changes in inputs $(x)$.

$$
\frac{\Delta y}{\Delta x} = \beta_1 + \beta_2 x
$$

### Inverse

The inverse model: $y = \beta_0 + \beta_1 \frac{1}{x} + \varepsilon$

* The effect of $x$ on $Y$ approaches 0 when $x \rightarrow \infty$

This model captures reciprocal relationship between the variables (such as in the original treatment of the Phllips curve). The model assumes that as $x \rightarrow \infty$, $y \rightarrow \beta_0 + \varepsilon$.

$$
\frac{\Delta y}{\Delta x} = \frac{-\beta_1}{x^2}
$$

### Combining functional forms

Even if the terminology talks about "functional forms", the above discussion looks at relationship between regressors. In other words, different "functional forms" can be combined into one model. Consider the following example with four different regressors.

$$
ln(y) = \beta_0 + \beta_1 x_1 + \beta_2 x_1^2 + \beta_3 ln(x_2) + \beta_4 \frac{1}{x_4} + \varepsilon
$$

In other words, picking the right "functional form" means picking the right relationship of **each** regressor with the correct representation of $y$.

### Functional forms in matrix notation

Matrix notation and OLS estimation does not change with different "functional forms" in each regressor. This is another reason why matrix notation is convenient, it helps keepings things simple and consistent. Consider the above example.


$$
\underbrace{
\begin{pmatrix}
    y_1     \\\\
    y_2     \\\\
    y_3     \\\\
    \vdots  \\\\
    y_N
\end{pmatrix}}_{y} =
\underbrace{
\begin{pmatrix}
    1       & x_{1,1} & x_{1,1}^2 & ln(x_{1,2}) & \frac{1}{x_{1,3}}  \\\\
    1       & x_{2,1} & x_{2,1}^2 & ln(x_{2,2}) & \frac{1}{x_{2,3}}  \\\\
    1       & x_{3,1} & x_{3,1}^2 & ln(x_{3,2}) & \frac{1}{x_{3,3}}  \\\\
    \vdots  & \cdots  & \cdots    & \cdots      & \vdots   \\\\
    1       & x_{N,2} & x_{N,1}^2 & ln(x_{N,2}) & \frac{1}{x_{N,3}}
\end{pmatrix}}_{X}
\underbrace{
\begin{pmatrix}
    \beta_0 \\\\
    \beta_1 \\\\
    \beta_2 \\\\
    \beta_3 \\\\
    \beta_4
\end{pmatrix}}_{\beta} + 
\underbrace{
\begin{pmatrix}
    \varepsilon_1 \\\\
    \varepsilon_2 \\\\
    \varepsilon_3 \\\\
    \vdots        \\\\
    \varepsilon_N
\end{pmatrix}}_{\varepsilon}
$$

### Summary

| Functional form | Equation                                        | Effect of $x$ on $y$ |
|-----------------|-------------------------------------------------|------------------|
| Linear          | $y = \beta_0 + \beta_1 x + \varepsilon$         | If $\Delta x = 1 \rightarrow \Delta y = 1$ |
| Log-Log         | $ln(y) = \beta_0 + \beta_1 ln(x) + \varepsilon$ | If $\Delta x = 1$% $\rightarrow \Delta y = \beta_1$% |
| Lin-Log         | $y = \beta_0 + \beta_1 ln(x) + \varepsilon$     | If $x$ |
| Log-Lin         | No serial correlation | $\rho(\varepsilon_i, \varepsilon_j) = 0 \; \forall i \neq j$|
| Polynomial      | Errors are homoskedastic | $\sigma_{\varepsilon, i} = \bar{\sigma_{\varepsilon}}$ |
| Inverse         | No multicollinearity | $\nexists \\; \omega_j \\; 

---

## Choosing the right functional form

---

## Example