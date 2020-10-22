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

OLS is the most common method to estimate the *parameters* of a linear regression such that the sum of the **square errors** are minimized. In more general terms, OLS is one application of a group of *linear least squares* methods.

Assume we want to estimate the linear relationship between mileage (mpg) $(Y)$ of autombiles with respect to its weight $(x_1)$. The dependent variable is $Y$ and $x_1$ is the regressor. Then, we are assuming that $Y$ has some sort of linear relationship with respect to its weight.

Let $n = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following.

$$ mpg_n = \beta_0 + \beta_1 weight_n + \varepsilon_n  $$
$$ Y_n = \beta_0 + \beta_1 x_{1,n} + \varepsilon_n $$

The error term $(\varepsilon)$ is capturing random situation that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude. 


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
	   title("Scatter plot: mileage versus weight", size(medium)) ///
	   mcolor(blue%50) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small))
	   
twoway scatter mpg length,											///
	   title("Scatter plot: mileage versus length", size(medium))	///
	   mcolor(red%50)												///
	   xlabel(, grid labsize(small)) xtitle(, size(small))			///
	   ylabel(, grid labsize(small)) ytitle(, size(small))
	   

*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="lecture 01\Fig 1.01.png" numbered="true" >}}  
{{< figure library="true" src="lecture 01/Fig 1.02.png" >}}

