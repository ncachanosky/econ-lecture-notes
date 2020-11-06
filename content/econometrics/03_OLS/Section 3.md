---
# Title, summary, and page position.
linktitle: "Evaluating the quality of a regression"
weight: 3

# Page metadata.
title: Evaluating the quality of a regression
type: book  # Do not modify.
---



---

## Methods to evaluate the quality of a regression

To evaluate how good an econometric model represents and matches the observed data requires considering several different issues. The proper evaluation of an econometric model requires an holistic approach. As is usual in econometrics, there are objective (numbers) and subjective (interpretation) issues at stake.

For instance, an econometric model of good quality should check the following boxes:

- [x] Does the model reflect sound economic theory?
- [x] Does the model include all the important regressors?
- [x] Are the estimated coefficients reasonable? Do their values contradict any economic theory or intuition?
- [x] Is the regression free of econometric problems? (later chapters)
- [x] How close to real data does are the model estimations? (this chapter)

This chapter deals with the last question. Namely, how good the *fit* of the model is. There are different ways to measure the goodness of fit of the model. First, we will go through the **coefficients of determination**. Second, we will go through three common **information criteria** indicators.

## Coefficients of determination

### Partition of sum of squares

Before building a measure of goodness of fit we need to decompose the variance of $y$ (the dependent variable) **around its mean**. The decomposition has three components.

First, the deviation of the observed data from its mean. The second one is the deviations that the model can predict of the dependent variable from its mean. And the third one is the residual, the difference between the difference between observed data and its mean and predicted data and the observed mean.

Since we are looking at **[variances](https://en.wikipedia.org/wiki/Variance)**[^1], these three measures will squared and added. Therefore, we have (1) the total sum of squares (TTS), (2) the explained sum of squares (ESS), and (3) the residual sum of squares (ESS). Then, the partition of sum squares is:

$$
\begin{align}
\overbrace{\sum_i (y_i - \bar{y})^2}^{\text{TSS}} &= \overbrace{\sum_i (\hat{y}_i - \bar{y})^2}^{\text{ESS}} + \overbrace{\sum_i (y_i - \hat{y}_i)^2}^{\text{RSS}} \\\\[10pt]
\sum_i (y_i - \bar{y})^2 &= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2
\end{align}
$$

This expression separates the total variance of the observed data between the explained and residual (non-explained) variance produced by the model. We can now build the $R^2$.

### The $R^2$ (R-squared)

$R^2$, the *[coefficient of determination](https://en.wikipedia.org/wiki/Coefficient_of_determination)* is the simplest and most common measure of goodness of fit. In simple terms, $R^2$ is the **ratio of the explained variations over total variations** of the dependent variable.

$$
\begin{aligned}
R^2 &= \frac{ESS}{TSS} \\\\
R^2 &= 1 - \frac{RSS}{TSS} \\\\
R^2 &= 1 - \frac{\sum e_i^2}{\sum (y_i - \bar{y})^2}, \in [0, 1]
\end{aligned}
$$ 

{{% callout note%}}
$\bar{R}^2$ measures the percent of the variations of $y$ arounds its mean by a regression.
{{% /callout %}}

The higher $R^2$ is, the closer the estimation $(\hat{y}_i)$ is to the real and observed data $(y_i)$. In plan words, $R^2$ measures the *percentage* of the variance of $y$ that the model can explain and has the following properties.

* Since $TSS = ESS + RSS$ and all three terms are positive, $R^2$ is between zero and one.
* Since OLS is minimizing $e^2$, your regression is getting the maximum $R^2$ possible given your data.

However, $R^2$ also has the following limitations:

* It does not inform if an important variable has been omitted
* It does not inform if the correct model (linear or otherwise) has been used
* It does not inform if the model is using the appropriate set of regressors
* It does not inform if you have enough data points to obtain an accurate estimation

Yet, there is another important shortcoming of $R^2$. The inclusion of a relevant regressors adds explanatory power to the model and makes $R^2$ increase (residuals are smaller). The addition of an irrelevant variables does not add, but neither subtracts, explanatory power from the model. In this case, $R^2$ does not change. Because of hot it is calculated, the addition of regressors can only increase (or do nothing) to the value of $R^2$.

This behavior of $R^2$ with respect to the number of regressors is a problem because the more regressors are included in the model, the more coefficients the model must estimate. This implies a loss in the [degrees of freedom](https://en.wikipedia.org/wiki/Degrees_of_freedom_(statistics)#:~:text=not%20present%20%20%20Continuous%20data%20%20,Biplot%20Box%20plot%20Control%20chart%20%20...%20) of the model. Degrees of freedom are the number of independent variables free to vary without affecting imposed constraints. More formally, degrees of freedom is the *minimum number of independent coordinates that can specify the position of the system completely*.

In econometrics, degrees of freedom are important as a measure of how much data is being used to produce an accurate estimation of the $betas$. Assume $N=10$ and your model needs to estimate 3 coefficients, then you have 7 observations to make such estimation. If you add three more regressors, now you have 6 coefficients but only 4 observations to calculate your model. The more data points you have *per* coefficient, the more accurate the estimation will be. Each regressor *substracts* one observation from your sample. You cannot have negative degrees of freedom, therefore the number of coefficients must be less than the sample size $(K<N)$

Adding regressors to a model is not free. Each regressor brings new explanatory power to the model at the cost of loosing a degree of freedom and accuracy. $R^2$ ignores the cost of adding regressors. Because adding more regressors to the model can never decrease $R^2$, you run the risk of *[overfitting](https://en.wikipedia.org/wiki/Overfitting)* your model. In short, overfitting occurs when the model tracks the data too close spuriously, that is the model uses residual data *as if* it were real data. This occurs when the model tries to specify more coefficients than can be justified with the data at hand.

Consider the regression where the mileage (mpg) of a car is predicted by its weight. We can add other relevent regressors such as the manufacturer, year of the car, type of car (sedan, SUV, sports car, and so on). We can also add an irrelevant variable, such as the first letter of name of their owners. This addition can bring some random (spourious) correlation with the mileage of the cars. $R^2$ will increase even if the *true* explanatory power of the model has not increase, you just added noise that is confused with *explanatory* power. 

The objective of a good econometric model is not to maximize $R^2$. That can be easily done by adding a large number of regressors. Yet, this will be a bad model because it may be overfitted and with inaccurate coefficients.

The role of the model is to find the **right** value of $R^2$. Ideally, the model will givea precise estimation of hoy much of the variations of $y$ can be explained with your regressors. An accurate estimation of what the **model does not explain** is valuable information as well that can lead to further research questions. Different subjects have different $R^2$. For instance, is likely to get a high $R^2$ with time-series because of correlation in time-trends. On the other hand, cross-sectional data looking at different countries may have a low $R^2$ because there are important differences across countries that are not easy to quantify.

This *inflation* of the $R^2$ is particularly problematic when comparing different models that have different number of regressors. The adjusted R-square, adj-$R^2$, or $\bar{R}^2$ is an extended version of $R^2$ that takes into account differences in degrees of freedom.

### The $\bar{R}^2$ (adjusted R-squared)

The $\bar{R}^2$ includes the trade-off between adding explanatory power (information) and loss of freedom. $\bar{R}^2$ only increases **if** the new regressors adds more information that the cost of loosing a degree of freedom. Assuming there are $K$ variables plus the constnat, then the degree of freedom adjustment works the following way

$$
\bar{R}^2 = 1- \frac{N-K-1}{N-1} \frac{RSS}{TSS}
$$

{{% callout note%}}
$\bar{R}^2$ measures the percent of the variations of $y$ arounds its mean by a regression, **adjusted by the degrees of freedom**.
{{% /callout %}}

Adding an irrelevant variable (no explanatory power) makes $\bar{R}^2$ decrease. The new regressor adds little information but harms the esimtation of the other regressors by reducing the amount of information (datapoints) availabe to estimate the $betas$.

---

## Information criteria

### Maximum likelihood

### AIC: Akaike Information Criterion

### BIC: Bayesian Information Criterion

### HQC: Hannan-Quinn Information Criterion

---

## Appendix

### Proof: $TSS = ESS + RSS$

$$
\begin{align}
\sum_i (y_i - \bar{y})^2 &= \sum_i (y_i - \bar{y} + \hat{y}_i - \hat{y}_i)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y}) + (y_i - \hat{y}_i) \right)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y}) + e_i \right)^2 \\\\[10pt]
&= \sum_i \left( (\hat{y}_i - \bar{y})^2 + e_i^2 + 2 \sum_i (y_i - \bar{y}) e_i \right) \\\\[10pt]
&= \sum_i (\hat{y}_i - \bar{y})^2 + \sum_i e_i^2 + 2 \sum_i e_i (\hat{\beta}_0 + \hat{\beta}_1 x\_{1,i} + ... + \hat{\beta}_K x\_{K,i} - \bar{y}) \\\\[10pt]
&= \sum_i (y_i - \hat{y})^2 + \sum_i e_i^2 + 2 (\hat{\beta}_0 - \bar{y}) \overbrace{\sum_i e_i}^{0} + 2 \hat{\beta}_1 \overbrace{\sum_i e_i x\_{1,i}}^{0} + ... + 2 \hat{\beta}_K \overbrace{\sum_i e_i x\_{K,i}}^{0} \\\\[10pt]
\underbrace{\sum_i (y_i - \bar{y})^2}\_{\text{TSS}} &= \underbrace{\sum_i (y_i - \hat{y})^2}\_{\text{ESS}} + \underbrace{\sum_i e_i^2}\_{\text{RSS}} \\\\[10pt]
\end{align}
$$


<!-- FOOTNOTES -->
[^1]: Recall that the variance of a **random** variable $x$ is: $\sum_i = p_i (x_i - \bar{x})^2$ (where $0 < p_i< 1$). If all values of $x$ have the same probability and there are $n$ observations, then $p_i = \frac{1}{n}$.