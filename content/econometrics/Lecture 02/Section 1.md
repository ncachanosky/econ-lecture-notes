---
# Title, summary, and page position.
linktitle: "Univariate regression"
weight: 1

# Page metadata.
title: Univariate regression
type: book  # Do not modify.
---


## What is Ordinary Least Squares (OLS)?

OLS is the most common method to estimate the *parameters* of a linear regression such that the sum of the **square errors** are minimized. In more general terms, OLS is one application of a group of *linear least squares* methods.

Assume we want to estimate the linear relationship between mileage (mpg) $(Y)$ of autombiles with respect to weight $(x_1)$ and the length $(x_2)$ of the car. The dependent variable is $Y$ and the two regressors (or independent) variables are $x_1$ and $x_2$. Then, we are assuming that $Y$ has some sorte of linear relationship with respect to these two regressors. 

Let $k = 1, ...,K$ be the number of regressors; in our case $K = 2$. Also, let $n = 1,...,N$ be the number of observations; that is, how many car observations we have with mileage, weight, and length we have at our disposal. The theoretical representation of this relationship is the following.

$$ mpg_n = \beta_0 + \beta_1 weight_n + \beta_2 length_n + \varepsilon_n  $$
$$ Y_n = \beta_0 + \beta_1 x_{1,n} + \beta_2 x_{2,n} + \varepsilon_n $$

The error term $(\varepsilon)$ is capturing random situation that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude. 

{{< figure src="Fig 01.png" title="A caption" >}}
{{< figure src="Fig 02.png" title="A caption" >}}

