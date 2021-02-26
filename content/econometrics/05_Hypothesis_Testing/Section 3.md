---
# Title, summary, and page position.
linktitle: "The F-test"
weight: 3

# Page metadata.
title: The F-test
type: book  # Do not modify.
---



---

## What does the $F$-test do?

The $t$-test is a single significance test in the sense that evaluates the statistical significance of one coefficient only. You can evaluate all the coefficients in your model, but you have to do so one at a time.

The $F$-test is a **joint** significance test. In this case the test considers if two or more coefficients are statistically significantly together, rather than individually.

Consider two examples where an $F$-test would be particularly useful. The first one is the case where the $t$-test for all your regressors fail to reject the null hypothesis that they are zero, but happens to be that all coefficients together (jointly) are significant.

The second example is when you have an hypothesis that involves more than one regressor. If you evaluating if there is any seasonality (such as quarterly) effect on a variable, then you need to jointly evaluate the coefficients for each seasonality included in the model. Looking at individual $t$-stats is not sufficient.

---

## Building the $F$-test

### The $F$ distribution

The $F$-statistic is the test-statistic of the $F$-test. If certain conditions hold, the $F$-statistic has the convenient [$F$-distribution](https://en.wikipedia.org/wiki/F-distribution) $(\chi^2)$.

The $F$-distribution typically arises when analyzing variances. More precisely, the $F$-distribution is the result of dividing to [Chi-square](https://en.wikipedia.org/wiki/Chi-square_distribution) distributions divided by their respective degrees of freedom.

A $\chi^2_n$ with $n$ degrees of freedom is the sum of $n$ squared standard normal distributions. Let $Z_i, ..., Z_n$ be $n$ standard normal distributions, then:

$$
\chi^2_n = Z_1^2 + ... + Z_n^2 = \sum_{i=1}^{n} Z_i^2 
$$

Then, the following variable $F$ has an $F$-distribution with $n_1$ and $n_2$ degrees of freedom:

$$
F = \frac{\chi^2_{n_1}/n_1}{\chi^2_{n_2}/n_2} \sim F_{n_1, n_2}
$$

Because the $F$-distribution is built with squared values, it can only take positive values. The shape of the $F$-distribution depends on the degrees of freedom.

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_04.png" >}}

### The $F$-statistic

Assume we have a model with $K$ regressors.

$$
y = \beta_0 + \beta_1 x_1 + ... + \beta_K x_K + \varepsilon
$$

The typical $F$-test has a **null hypothesis** were the coefficient of all variables are zero (except the intercept). The **alternative hypothesis** is that at least one coefficient is different than zero; even if the $F$-test cannot indicate which coefficient(s) is(are) different than zero.

$$
\begin{align}
H_0&: \beta_1 = ... = \beta_K = 0 \\\\[10pt]
H_A&: \text{otherwise}
\end{align}
$$

Different versions of the $F$-test can be constructed, where only selected coefficients are assumed to be zero. For instance, an $F$-test for coefficients 1, 4, and 5 will look the following way:

$$
\begin{align}
H_0&: \beta_1 = \beta_4 = \beta_5 = 0 \\\\[10pt]
H_A&: \text{otherwise}
\end{align}
$$

How can the **joint significance** be tested? To look at the statistical significance of more than one coefficient at the time, the $F$-test compares the $SSR$ of the model with all the coefficients with the $SSR$ of the model assuming $H_0$ is true.

Imposing a value of zero for some coefficients will increase the $SSR$. If the difference between the $SSR$ is large enough, then it is unlikely that all the coefficients included in the test are zero, at least one of them should be statistically significant. However, if the $SSR$ of both models are similar to each other, then it is more unlikely that we can reject the null hypothesis.

In other words, as long as the coefficients are **jointly** significant, the SSR of the model should be significantly less than the $SSR$ of the model imposing the restriction that those coefficients must equal zero.

The $F$-statistic is built following this logic. Assume you are testing if $M$ coefficients are equal to zero. 

$$
F_{d_1, d_2} = \frac{(SSR_M - SSR)/M}{SSR/(N-K-1)} \sim F_{M, N-K-1}
$$

The numerator is taking the difference between the $RSS$ of each model, divided by the number of restrictions (how many coefficients are included in $H_0$). The denominator is looking at the $SSR$ of the original model, free of restrictions on the coefficients divided by the degrees of freedom of the model. The sample size $(N)$ is substracted the number of variables $(K)$ and the constant (which is the number $1$).

The reason this statistic has an $F$-distribution is because the $SSR$ is the sum of squared residuals, which have a normal distribution. Therefore, $SSR$ has a $\chi^2$ distribution. As mentioned above, the ratio of two $\chi^2$ distribution divided by their respective degrees of freedom yields an $F$-distribution.

{{% callout warning %}}
**Condition for the $F$-test to have an $F$-distribution**

* The residuals must have a normal distribution with zero mean
* If the residuals do not have a normal distribution, then the $SSR$ does not have a $\chi^2$ distribution and therefore the $F$-statistic does not have an $F$-distribution
 
---

If the errors do not have a normal distribution, then the $F$-test **is invalid**
{{% /callout %}}

### Example

