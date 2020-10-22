---
# Title, summary, and page position.
linktitle: "Univariate regression"
weight: 1

# Page metadata.
title: Univariate regression
type: book  # Do not modify.
---

---
## What is Ordinary Least Squares (OLS)?

[OLS](https://en.wikipedia.org/wiki/Ordinary_least_squares) is the most common method to estimate the *parameters* of a linear regression such that the sum of the **square errors** is minimized. In more general terms, OLS is one application of a group of *linear least squares* methods.

Assume we want to estimate the linear relationship between mileage (mpg) $(Y)$ of autombiles with respect to its weight $(x_1)$. The dependent variable is $Y$ and $x_1$ is the regressor. Then, we are assuming that $Y$ has a linear relationship with respect to its weight.

Let $n = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following.

$$ mpg_n = \beta_0 + \beta_1 weight_n + \varepsilon_n  $$
$$ Y_n = \beta_0 + \beta_1 x_{1,n} + \varepsilon_n $$

The error term $(\varepsilon)$ is capturing random situation that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude.

Let's use the 1978 automobile dataset in `STATA` and run a [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) between mileage and weight. The following `STATA` code will produce the scatter plot ([Figure 1](#Figure--scatter-plot-mileage-versus-weight)). The dataset has 74 observations, therefore the scatter plot will have 74 points (mileage-weight relationships).


```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific	// Set plot scheme
sysuse auto				// Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
	   mcolor(blue%50) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small))
	   
*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```
{{< figure library="true" src="lecture 01/Fig 1.01.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  


