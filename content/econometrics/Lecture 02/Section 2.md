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

For instance, let the price of houses be the dependent variable $(Y_i)$. The price of the house does not depend only on the size of the house. It also depends on other variables such as how old the house is, distance to highways and public trnansportation, quality of the district high-school, location of the neighborhood, safety, and so on. Let $j = 1, ..., K$ be the number of regressors; then:

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

### Multiple coefficients ($betas$)
Because the model includes multiple regressors, the model also includes multiple coefficients. Because of this, a word of caution is needed.

The temptation to compare the *size* of the betas must be avoided. The fact that one coefficient is larger than another does not mean is more important or even that that variable is having a larger effect on the dependnet variable. There are two reasons why this happens.

The first one is that the size of the $betas$ depend on the unit of measure of the regressor. In the above example, the size of $\beta_1$ will be different if the size of the house is measured in units of squared foots or in hundreds of square foots. If you transform the size of the house from units into hundreds, then its coefficient will be hundred times smaller (for instance, it will fall from 200 to 2). Therefore, the relative size of the coefficient depend on what unit of measure is being used in the coefficients.

The second reason is that regressor attached to a $beta$ with a high value may depict very little variability, while another regressors with more varibility is attached to a $beta$ with a lower value. In other words, a high $beta$ may not produce much of an effect on $Y$ because its regressor hardly moves, while another $beta$ with a lower value is attached to a regressor that moves more. This is why you may want to consider not just the value of the $betas$, but the $betas$ times the standard deviation of its regressor: $\beta_i \cdot \sigma_(x_1)$.

### What is the meaning of the intercept ($\beta_0$)?
The mathematical intepretation of $\beta_0$ is straightforward. It is the expected value of $Y$ when **all** regressors are equal to zero $(x_1 = ... = x_6 = 0)$. 

The conceptual intepretation of $\beta_0$ is a little more challenging. In the above model, if all the regressors are zero, then a house with zero size located directly over a highway will have some positive expected value. The issue is that $beta_0$ is merging several components of the regression model. Inside $\beta_0$ we have:

1. The true value of $\beta_0$ (which may or may not be equal to zero)
1. A *constant impact* of any specification error (the equation of the model is wrong).
1. The mean of $\varepsilon$ conditional on your model being correctly specified. 

We can translate this into simpler terms. Remember that OLS is fitting the line that minimizes the squared residuals. This line has two components, the *slope* of the line and its *level* (or intercept). OLS is not just about finding the right slope, is also finding the right vertical location of the best line. 

If you drop from the equation the constant term because it has no clear economic meaining, you run the risk of mispecifying your model. Droping the constant term is forcing the model to find the best slope when the interepct is zero. 

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

The blue dashed line is the best estimation, the one that minimizes the squared residuals. The green solid line is the estimation that drops the constant. As mentioned above, dropping the constnat is telling the model you want the constnat to be zero, therefore OLS will estimate the slope that minimizes the squared errors **conditional** on the constant being zero (if your project the line all the way to the left it will cross the $(0, 0)$ point). In this example the effect is not just slightly different slope, but an opposite sign. The best line has a negative slope, but by setting the constant to be zero now the model estiamtes a positive relationship between weight (lbs.) and mileate (mpg). 

The reason to keep the constant in your model is not because of its economic intepretation, if it has any. The reason is that by having OLS the option to also estimate the constnat it has more variables at its disposal to find the best line possible. The best line is constructed with **two** variables, *slope* and *intercept*.

---
## Why do a multivariate regression


---
## Algebraic solution


---
## Example