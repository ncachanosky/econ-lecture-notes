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

Recall that a regression **estimates** a value of an unobserved/unknown **true** $beta$. Because $\hat{\beta}$ is an estimation it has a probability distribution.

Every different sample taken from the same population will produce different values of $\hat{\beta}$. From all the potential different samples you can get, you get to work with only one. That is, from all the potential different values of $\hat{\beta}$ you can calculate, your regression will only give you one $beta$. Therefore, it is important to understand the $\hat{\beta}$ distribution.

A good sample and a good estimation technique will increase the likelihood that the $\hat{\beta}$ you estimate will be close to the true $\beta$. To understand how this works, we need to have a closer look at the OLS coefficient estimation.

Recall that (using matrix notation):

$$
\begin{aligned}
y =& X\beta + \varepsilon \\\\[10pt]
\text{and} \\\\[10pt]
\hat{\beta} =& \left( X'X \right) ^{-1} X'y
\end{aligned}
$$

Use now the first equation into the second one (where $I$ is the identity matrix):

$$
\begin{aligned}
\hat{\beta} =& \left( X'X \right)^{-1} \left(X'X \right) \beta + \left(X'X \right)^{-1} X \varepsilon \\\\[10pt]
\hat{\beta} =& I \beta + \left(X'X \right)^{-1} X \varepsilon \\\\[10pt]
\hat{\beta} =& \beta + \left(X'X \right)^{-1} X \varepsilon
\end{aligned}
$$

You can see that because $\varepsilon$ is a random variable, so is each $\hat{\beta_i}$. Therefore, your $\hat{\beta}$ has a mean and a standard deviation. Mean and deviation are related to the concept of unbiased and efficiency respectively. You can also see that your $betas$ have the same distribution than $\varepsilon$ (recall the classical model assumption 7).

---

## Unbiasedness and Efficiency

### Unbiasedness

An estimation is unbiased if its expected value coincides with the true value under estimation. You have a biased estimation when the expected value of the estimation diverges from the true value under estimation.

Consider the following example. The bullseye of a target represents the true value that your are trying to estimate. The darts you through are your econometric estimations. If your darts miss but fall around the target, your estimations are unbiased. If you average all your estimations you get the true value you are trying to estimate (errors cancel out). However, if your darts fall (in average) to either side of the target, then your estimation is biased. You tend to err more to one side such that if you average all your estimations you do not get the true value under estimation.

We can represent an unbiased and biased estimation in the following way:

1. Unbiased estimation: $E[\hat{\beta}] = \beta$
2. Biased estimation: $E[\hat{\beta}] = \beta + \xi, \; \xi \neq 0$

You already know that your estimation will probably not be just on target. It is very unlikely you will get the **true** $beta$. But, you **do not want** your estimation to be biased. You are going to miss the bullseye, but you want to aim right be as close to your target as possible. Remember, in a regression you get to through only only one dart, you want to make it count.

If assumptions 1 to 6 of the classical model hold $(\rho(X,e)=0$ and $E[\varepsilon]=0)$, then OLS produces unbiased estimators.

$$
\begin{aligned}
\hat{\beta} =& \beta + \left(X'X \right)^{-1} X' \varepsilon \\\\[10pt]
E[\hat{\beta}] =& E \left[ \beta + \left(X'X \right)^{-1} X' \varepsilon \right] \\\\[10pt]
E[\hat{\beta}] =& \beta + \left(X'X \right)^{-1} X' \underbrace{E[\varepsilon]}\_{0} \\\\[10pt]
E[\hat{\beta}] =& \beta
\end{aligned}
$$

### Efficiency

Efficiency relates to how close or far from the **true** beta estimations fall, even if in average your estimations are unbiased. The lower (higher) the variance of an estimation, the more (less) estimations will be close to the **true** value under estimation. In our above throwing-darts example, the distance between the dart represent the standard deviation of your estimation technique.

Let's assume $\beta = 0$ and you have two sets of two estimations. The **first** set of estimations yields $(\hat{\beta}\_{1,1}, \hat{\beta}\_{1,2}) = (-1, 1)$. The second **set** of estimations yields $(\hat{\beta}\_{2,1}, \hat{\beta}_{2,2}) = (-2, 2)$. Both sets of estimations give, in average, the true $\beta$. However, the first set of estimations is better in the sense that the estimated values are closer to the true $\beta$ than those of the second set of estimations.

To evaluate the efficiency of the OLS estimation we need to apply the variance $(V)$ operator.

$$
\begin{aligned}
\hat{\beta} =& \left( X'X \right)^{-1} X' \varepsilon \\\\[10pt]
V[\hat{\beta}] =& V \left[ \left( X'X \right)^{-1} X' \varepsilon \right] \\\\[10pt]
V[\hat{\beta}] =& \left( X'X \right)^{-1} X' \\; V[\varepsilon] \\; X \left( X'X \right)^{-1} \\\\[10pt]
V[\hat{\beta}] =& \left( X'X \right)^{-1} X' \left(I \sigma^2_{\varepsilon} \right) X \left( X'X \right)^{-1} \\\\[10pt]
V[\hat{\beta}] =& \sigma^2_{\varepsilon} \left( X'X \right)^{-1} \\\\[10pt]
\end{aligned}
$$

The efficiency of $\hat{\beta}$ depends not only on $\left(X'X\right)$, but also on the variance of the errors $(\sigma^2\_\varepsilon)$. The efficient estimation is the one that produces the lowest possible variance of your estimated $betas$.

### Bias and efficiency plotted

The following plot depicts different scenarios. The <span style="color:blue">blue</span> line depicts the distribution of an unbiased and efficient estimation of $\beta$. You can see that the mean of this estimation coincides with the true $\beta$. The <span style="color:green">green</span> line depicts the distribution of an unbiased but inefficient estimation of $\beta$. You can see that, with respect to the <span style="color:blue">blue</span> estimation, is less likely that you will get the true $\beta$ and more likely that you will get an estimation farther away from the true value. Finally, the <span style="color:red">red</span> line depicts the distribution of estimation that is both biased and inefficient. It is biased because its expected value has a $\xi \neq 0$ deviation from the true $\beta$. It is inefficient because it has a larger variance than the <span style="color:blue">blue</span> estimation.

{{< figure library="true" src="econometrics/04_Classical_Model/Fig_02.png" >}}