---
# Title, summary, and page position.
linktitle: "The t-test"
weight: 2

# Page metadata.
title: The $t$-test
type: book  # Do not modify.
---



---

## What does the $t$-test do?

The $t$-test is a s typical test used to test the null hypothesis that a coefficient is different than zero. If this is the case, then the *marginal effect* of its regressors is different than zero and, therefore, said regressor has some explanatory power over the variations of the dependent variable. If the coefficient of a regressor were to be zero $(\beta = 0)$, then said regressor is unrelated with the dependent variable.

A coefficient different than zero can follow in any of the three following categories (number three is unlikely, but not impossible):

1. The regressor is economically significant
2. The regressor is economically insignificant
3. The regressor adds information, but not enough to compensate the loss of degrees of freedom (for instance, $\bar{R}^2$ decreases)

In its most common specification, the $t$-test null hypothesis is that a coefficient is different than zero (two-tailed test), regardless of the sign. An alternative specification would be to test of a given coefficient is positive or negative (one-tailed test).

---

## Building the t-test

### The Student's $t$-distribution

The **t-statistic** is the test-statistic of the $t$-test. The t-statistic has a [Student's t-distribution](https://en.wikipedia.org/wiki/Student%27s_t-distribution).

The t-distribution captures the probability distribution when estimating the mean of a normally-distributed population when (1) the sample size is small and (2) the standard deviation is unknown. Visually, the t-distribution looks like a normal distribution with higher tails.

The exact shape of the t-student distribution depends on the degrees of freedom of your model. The larger the degrees of freedom, the more similar to the standard normal distribution the t-distribution looks like.

{{% callout warning %}}
For the $t$-test to be a valid test, $\hat{\beta}$ must have a normal distribution. From our previous chapter we know that for $\hat{\beta}$ to have a normal distribution, the errors must have a normal distribution.

If the errors **do not** have a normal distribution, then you cannot do a $t$-test.
{{% /callout %}}

### The t-statistic

If your model has a constant and $K$ regressors, then you will have $K+1$ t-tests, one **independent** test for each coefficient. 

Let the null hypothesis be $\beta_j$ $(j = 0, ..., K)$, $t_j$ be the t-statistic of each test, $t_C$ be the critical (threshold) value, and $DF$ be the degrees of freedom. Then:

$$
\begin{aligned}
H_0 :& \beta_j = 0 \\\\[10pt]
H_A :& \beta_j \neq 0 
\\\\[10pt]
t_j =& \frac{\hat{\beta}_{j} - 0}{\hat{\sigma}_{\hat{\beta}}} \sim t_{DF}
\end{aligned}
$$

Each $t$-test is *solved* by comparing the value of $t_j$ with the value of $t_C$ (that depends on your confidence level $\alpha$). Alternatively, you can compare the p-value of each $t_j$ with your desired confidence value.

If you look at the denominator, you will see that the t-statistic is built with the **estimation** of the standard deviation of the estimated coefficient.

### Example

Let's look again at our first regression.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 06.png" >}}

We can now make sense of the data to the right of **each** coefficient. The `Std. Err.` is the estimated standard error of each coefficient $(\hat{\sigma}_{\hat{\beta}})$ (that is, the numerator of the t-statistic). The column that follows (`t`) are the values of the t-statistics; because the null hypothesis is $\beta=0$, you can see that $t_j = \hat{\beta}/\hat{\sigma}_{\hat{\beta}}$. The next piece of information are the `p-values` associated with each $t_j$. As you can see, it is easier to compare the p-values with your desired level of $\alpha$ than comparing each $t_j$ with the $t_C$ (which needs to be estimated for each different value of degrees of freedom). Finally, the `confidence interval` is calculated making use of the standard error of each coefficient.

---

## Limitations of the $t$-test

