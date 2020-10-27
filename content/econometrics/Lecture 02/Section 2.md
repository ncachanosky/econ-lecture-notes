---
# Title, summary, and page position.
linktitle: "Multivariate regressions"
weight: 2

# Page metadata.
title: Multivariate regressions
type: book  # Do not modify.
---

---
## What is a multivariate regression

### Multiple regressors
It is very unlikely that a dependent variable can be properly *explained* (in the econometrics sense) by a single regressors. In most cases a regression analysis will use several regressors.

For instance, let the price of houses be the dependent variable $(Y_i)$. The of housees obviously depends on its size. But, it also depends on other variables such as how old the house is, distance to highways, quality of the district high-school, location of the neighborhood, safety, and so on. Let $j = 1, ..., K$ be the number of regressors; then:

1. $x_1$: size of the house,
1. $x_2$: age of the house,
1. $x_3$: distance to highways and public transportation,
1. $x_4$: high-school quality in the area,
1. $x_5$: neighborhood location,
1. $x_6$: safety.

In this case we have 6 regressors, which can be used to build the following theoretical linear relationship:

$$ Y_i = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_4 x_4 + \beta_5 x_5 + \beta_6 x_6 + \varepsilon $$

The estimated model will be:

$$ \hat{Y_i} = \hat{\beta_0} + \hat{\beta_1} x_1 + \hat{\beta_2} x_2 +
\hat{\beta_3} x_3 + \hat{\beta_4} x_4 + \hat{\beta_5} x_5 + \hat{\beta_6} x_6 $$

Now the expected (estimated) value of the house depends on value observed in a number of variables (size, age of the house, location, etc.) As long as the regressors included in the model are relevant to explain the price of a house, then this model will be more precise than a model with only one regressor. 

We now moved from a model with $N$ observations and 1 variable, to a model with $N$ observations and $K$ variables.

### Multiple coefficients ($betas$)
Since the model includes multiple regressors, the model also has multiple coefficients. Because of this, a word of caution is needed.

The temptation to compare the *size* of the betas must be avoided. The fact that one coefficient is larger than another does not mean is more important, nor that that variable is having a larger effect on the dependnet variable. There are two reasons why this happens.

The first one is that the size of the $betas$ depends on the unit of measure of the regressor. In the above example, the size of $\beta_1$ will be different if the size of the house is measured in units of squared foots or in hundreds of square foots. If you transform the size of the house from units into hundreds, then its coefficient will be hundred times smaller (for instance, it will fall from 200 to 2). Therefore, the relative size of the coefficient depends on what unit of measure is being used in the coefficients.

The second reason is that a regressor attached to a $beta$ with a high value may depict very little variability, while another regressors with more varibility is attached to a $beta$ with a lower value. In other words, a high $beta$ may not produce much of an effect on $Y$ because its regressor hardly moves, while another $beta$ with a lower value is attached to a regressor that moves more. This is why you may want to consider not just the value of the $betas$, but the $betas$ times the standard deviation of its regressor: $\beta_i \cdot \sigma_{x_1}$.

### What is the meaning of the intercept ($\beta_0$)?
The mathematical intepretation of $\beta_0$ is straightforward. It is the expected value of $Y$ when **all** regressors are equal to zero $(x_1 = ... = x_6 = 0)$. 

The conceptual intepretation of $\beta_0$ is a little more challenging. In the above model, if all the regressors are zero, then a house with zero size located directly over a highway will have some positive expected value. The issue is that $\beta_0$ is merging several components of the regression model. Inside $\beta_0$ we have:

1. The true value of $\beta_0$ (which may or may not be equal to zero)
1. A *constant impact* of any specification error (the equation of the model is wrong).
1. The mean of $\varepsilon$ conditional on your model being correctly specified. 

We can translate this into simpler terms. Remember that OLS is fitting the line that minimizes the squared residuals. This line has two components, the *slope* of the line and its *level* (or intercept). OLS is not just about finding the right slope, is also about finding the right vertical location of the best line. 

If you drop from the equation the constant term because it has no clear economic meaning, you run the risk of mispecifying your model. Droping the constant term is forcing the model to find the best slope when the interepct is zero: $Y_i = 0 + \beta_1 x_1 + \varepsilon$.  

The effect of dropping the constant can be seen in the plot below. Let's use again the automobile information from the previous section and add to the scatter plot two regression lines. One with an estimated constant, and a second one with no constant.

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Multivariate regression
* Code sample: 2.4
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific  // Set plot scheme
sysuse auto  // Load 1978 Automobile Data from STATA

regress mpg weight, noconst
predict y_hat, xb
label variable y_hat "No constant"

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
	   mcolor(blue%50) ///
	   xlabel(0(500)5000) ///
	   ylabel(0(5)40) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small)) ///
	 ||lfit mpg weight, ///
	   lcolor(blue%50) ///
	 ||line y_hat weight, ///
	   lstyle(solid) lcolor(green%50) ///
	   legend(position(6) rows(1) size(vsmall))
	   
*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/lecture 02/Fig 2.04.png" numbered="true" title=" Scatter plot: The effect of dropping the constant term">}}  

The blue dashed line is the best estimation, the one that minimizes the squared residuals by estimating both the constant and the slope of the fitted line. The green solid line is the estimation that drops the constant and only estimates the slope. As mentioned above, dropping the constnat is telling the model you want the constnat to be zero, therefore OLS will estimate the slope that minimizes the squared errors **conditional** on the constant being zero (if you project the green line all the way to the left it will cross the $(0, 0)$ point). In this example, the effect is not just a slightly different slope, but having the opposite sign. The best line has a negative slope, but by setting the constant to be zero now the model estimates a positive relationship between weight (lbs.) and mileate (mpg). 

The reason to keep the constant in your model is not because of its economic intepretation, if it has any. The reason is that by having OLS the option to also estimate the constnat it has more variables at its disposal to find the best line possible. The best line is constructed with **two** variables, *slope* and *intercept*.

---
## Why do a multivariate regression
The above discussion already points to a reason for preferring a multivariate regression over a univaraite regression. We can have a better estimation of the dependent variable because we can use more data related to the price of houses. We know now that OLS is fitting a line that minimizes the squared residuals, in the next section we will see in more detail how to *measure* the quality of the fitted line.

However, there are other two important reasons of why multivariate regression are preferred over univariate regression. The role of control variable and to avoid the serious problem of ommited variable bias.

### Control variables
Let's assume we run a univariate regression, where the price of houses is the dependent variable and the size of the house is the regressor. The model will find the best fit using this single regressor. However, the coefficient of the size of the house **does not capture** the *ceteris *paribus* relationship between the price and size of houses. 

The problem is that when OLS is looking at two houses, they may differ in other variables other than price and size. Maybe one house is better located than the other or is closer to a highway. In other words, the regression is *implicitly* affected by all changes in all variable. 

To avoid this issue, the model must include *all* variables we want to hold constant, as if we were in a chemistry lab. If we add a second regressor looking at the age of the house, then OLS can look at the impact of size on price *keeping the age of the house constant*. This is why regressors are also referred as **control variables**, because they control variation on other variables allowing to read a coefficient as the effect of its regressors *maintaiing all other variables constant*.

We can split the regressors into two groups. On one side, those regressors of which we are interested in estimating their marginal effects (the coefficients). On the other side, those regressors which we have no interest in the value of their coefficients, but we need them in the model to serve as control variables such that we can properly intepret the coefficient of the variables of interest. Let $x_i$ denote the vriables of interest and $z_j$ denote the control variables. Then, the model can be represented the following way.

$$

Y_i = \beta_0 + \underbrace{\beta_1 x_1 + ... + \beta_4 x_4}_\text{variables of interest} + \underbrace{\gamma_1 z_1 + ... + \gamma_7 z_7}_\text{control variables} + \varepsilon

\end{align}
$$

### Avoid ommitted variable bias

---
## Algebraic solution


---
## Example