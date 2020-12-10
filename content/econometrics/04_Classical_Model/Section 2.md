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

This assumption requires the model to be **linear** and, of course, be correctly specified (are you forgetting any important regressor?) However, we need to be careful with what we mean by **linear** in this context.

The following is a typical linear model with an additive error term:

$$
y_i = \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \varepsilon_i
$$

The expression **linear model** can be confusing. We tend to think in *math terms*, where a linear equation is one with **linear variables**, that is, elevated to the power 1: $y = a + b_1 x_1 + b_2 x_2 + b_3 x_3$.

However, the classical assumption requires the model to be linear on the **coefficients**. As long as there are independent additive terms with linear coefficients, then the model is linear. Remember that what we are estimating is the $betas$, no the regressors.

Consider two examples of non-linear regressors. Let the first one has squared regressors $(w_i^2)$ and the second one has logarithmic regressors $(ln(w_i))$ regressors. In both cases, regressors are no linear. These two examples are easy to linearize, just define $x_i = w_i^2$ in the first model and $x_i = ln(w_i)$ in the second model. Then:

$$
\begin{aligned}
y_i =& \beta_0 + \beta_1 \underbrace{z_i^2}\_{x_1} + ... + \beta_k \underbrace{x_K^2}\_{x_K} + \varepsilon_i \\\\[10pt]
y_i =& \beta_0 + \beta_1 \underbrace{ln(z_1)}\_{x_1} + ... + \beta_k \underbrace{ln(z_K)}\_{x_k} + \varepsilon_i
\end{aligned}
$$

*Econometrically speaking*, both models are identical in the sense that both are linear and with the same number of regressors. Of course, since we are looking at different data the estimated $betas$ will differ. Yet, both models are identical in the sense of how $betas$ are estimated.

Consider now a non-linear **theory** that can be linearized before running your regression. For instance, your theory may be represented by the following equation:

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

In general terms, a model linear in the coefficients has the following functional form:

$$
f(y) = \beta_0 + \beta_1 f(x_1) + ... + \beta_K f(x_K)
$$

An example of a model non-linear in the coefficients would be $y = \beta_0 + x_1^{\beta_1} + ... + x_k^{\beta_K}$. There is no arrangement that would make this equation linear on the $betas$.

There two other important conditions in this assumption:

1. The model is correctly specified, meaning there is no **omitted variables**
2. The error term is additive to the model and cannot be multiplied by or divided by any other regressor(s) included in the model

{{% callout note %}}
**Assumption 1** requires that:
1. Your econometric model can be represented as a model linear *on the coefficients*, even if the regressors do not have a linear behavior or if the underlying theory is not linear
2. All important regressors are included in the model
3. The error can be represented as an additive term independent of all regressors
{{% /callout %}}

---

## Assumption 2: The error term has zero population mean

The error term, which has a random or stochastic behavior, captures variations of the dependent variable unexplained by the regressors. Each observation has its own error term. Assumption 2 requires the mean of the errors to be zero (where $E[\cdot]$ denotes the expected value):

$$
E[\varepsilon] = 0
$$

The intuition behind this asspmition is that errors should cancel out. The following figure depicts the distribution of an hypothetical error term. You can see that the mean is zero with <span style="color:red">negative</span> and <span style="color:blue">positive</span> errors. You can also see that the majority of the errors are small (close to zero) and only a few errors are large (far away from zero). **Importantly**, even though the error term in the figure looks like it has a normal distribution, Assumption 2 does not require errors to have a normal distribution, only to have a zero mean value. However, a normal distribution of the errors is a desirable condition (wait until Assumption 7).

{{< figure library="true" src="econometrics/04_Classical_Model/Fig_01.png" >}}

To be more price, assumption 2 builds over an asymptotic condition. In a small sample, it is possible that the mean of the error term is not exactly equal to zero. What is required is that the mean of the error term converges to zero as the sample size increases to infinity $(n \rightarrow \infty \therefore E[\varepsilon] \rightarrow 0)$

Assumption 2 is another reason to include a constant term in your model. Assume the mean of the error term has a non-zero value (positive or negative) of $\xi \neq 0$. Then you can re-write your model in the following way:

$$
\begin{aligned}
y_i =& \left(\beta_0 - \xi \right) + \beta_1 x_{1,i} + ... + \beta_K x_{k,i} + \left(\varepsilon_i + \xi \right) \\\\[10pt]
y_i =& \beta^*_0 + + \beta_1 x_{1,i} + ... + \beta_K x_{k,i} + \varepsilon^*_i
\end{aligned}
$$

where $\beta^\*\_0 = \beta_0 - \xi$ and $\varepsilon^\*\_i = \varepsilon_i + \xi$.

Therefore, your model will fulfill assumption 2 as long as it has a constant term. In other words, the constant term will move up or down as necessary to guarantee that $E[\varepsilon]=0$.

{{% callout note %}}
**Assumption 2** requires that:
1. The mean of the error term is zero: $E[\varepsilon]=0$
2. No requirement is made on the standard deviation $(\sigma)$ or type of distribution of error term
{{% /callout %}}

---

## Assumption 3: All explanatory variables are uncorrelated with the error term

All regressors should be uncorrelated with the error term. Let $\rho$ denote correlation, then:

$$
\rho(x_j, e) = 0 \\;\\;\\;\\; \forall j = 1, ..., K
$$

If this condition is violated, then the estimation of the coefficients of the regressors included in the model may be biased. Every omitted variable is part of the error term. Assume you forget to include regressor $z_i$ in your model. If the pure error term is $\varepsilon$, then the error term of your model becomes $\varepsilon^* = \varepsilon + \gamma z_i$.

$$
\begin{aligned}
y+i = \beta_0 + \beta_1 x_{1,i} + ... + \beta_K x_{K,i} + \underbrace{\left(\varepsilon_i + \gamma z_i \right)}_{\varepsilon^*} 
\end{aligned}
$$

If $\gamma \neq 0$, then you have omitted a significant variable (otherwise, if $\gamma = 0$, then $\gamma z_i = 0$). Omitting $z$ can lead to a miscalculation of the other regressors. If $\rho(x_j,z) \neq 0$ for any $j$, then $\rho (x_j, \varepsilon^*) \neq 0$.

If any of the regressor is correlated with $z$ (a likely situation in economics), then assumption 3 will be violated. Even if $\rho (x_j, \varepsilon^*) = 0$, it is still the case that in your model $\rho (x_j, \varepsilon) \neq 0$ because $\varepsilon$ includes $z$, which is correlated with one ore more of your regressors.

If $\rho (x_1, z) > 0$, then you should expect for $\hat{\beta_1}$ to capture not only the effect of $x_1$ on $y$, but also some of the effect of $z$ on $y$. Therefore your model will have an *upward* (or positive) bias when estimating $\hat{\beta_1}$. If $\rho (x_1, z) < 0$, then the situation is the opposite.

It is possible, but unlikely, that $\gamma > 0 \wedge \rho (x_j, z) = 0 \; \forall j = 1, ..., K$. In this hypothetical case, omitting a significant variable has no effect on the estimation of the other regressor's coefficients.

Another situation likely to violate assumption 3 is when your model has an independent variable with a simultaneous relationship with at least one regressor. This means that there is a two-direction causal effect between $y$ and $x_j$. This is the problem of **endogeneity**. The regression requires that the causal effects goes from $x \to y$. But, if the relationship is mutual $(x \leftrightarrow y)$, then your model suffers from endogeneity and coefficient estimation will be biased. This **system of equations** requires a joint estimation rather than independent models.

{{% callout note %}}
**Assumption 3** requires that:
1. All regressors are uncorrelated with the error term: $\rho (x_i, \varepsilon) = 0 \\;\\;\\;\\; \forall j = 1, ..., K$  
This assumption is usually violated in two situations:
* You omit a significant variable, which is correlated with at least one regressors included in the model
* Your model has a bi-directional causal effect (simultaneity) between the independent variable and at least one of the regressors
{{% /callout %}}

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