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

Assume we want to estimate the linear relationship between mileage (mpg) $(Y)$ of autombiles with respect to its weight $(x)$. The dependent variable is $Y$ and $x$ is the regressor. Then, we are assuming that $Y$ has a linear relationship with respect to its weight.

Let $n = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following.

$$
\begin{align}
mpg_n &= \beta_0 + \beta_1 weight_n + \varepsilon_n \\\\[10pt]
Y_n   &= \beta_0 + \beta_1 x_n + \varepsilon_n
\end{align}
$$

The error term $(\varepsilon)$ is capturing random situation that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude.

Let's use the 1978 automobile dataset in `STATA` and run a [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) between mileage and weight. The following `STATA` code will produce the scatter plot ([Figure 1](#figure--scatter-plot-mileage-versus-weight)). The dataset has 74 observations, therefore the scatter plot will have 74 points (mileage-weight relationships).


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
{{< figure library="true" src="econometrics/lecture 01/Fig 1.01.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  

We can draw an infinite number of lines that go through the scatter plot. But, we are not looking for *any* line, we are looking for a line that would minimize errors on the prediction of mileage when looking at the weight of a car. OLS is a method to efficiently fit a line through those 74 points. 

---
## The OLS method
### What is OLS doing?
We need to find the values of $\beta_0$ and $\beta_1$ that would minimize estimation mistakes. Once we have estimated values for our $betas$, we can use the $weight$ data to predict $mileage$. 

$$ \hat{Y_n} = \hat{\beta_0} + \hat{\beta_1} x_n $$

{{% callout warning %}}
Do not confuse the **error** term with the **residual**.
{{% /callout %}}

Before proceeding, is important to distinguish betweeen the **error** term $(\varepsilon)$ and the **residual** $(e).$ The *residual* captures the random events that produce a difference between weight and mileage. Because this is a random variable (for instance changes in weather) the residual is also referred as the **stochastic residual** term. The residual is unobservable. If all these random events were known, then we would be able to add them to the model. The *error* term is the difference between the model prediction and the real world data. In this sense is like a *proxy* of the unovserbable residual. Because the error is unobservable, OLS minimizes the residual.

More precisely, the residual equals: $e_n = Y_n - \hat{Y_n}$. For instance, after you estimate the $betas$ of the equation, a weight of 2000 pounds predicts a mileage of 27 mpg. However, you know that a car with a weight of 2000 pounds has a mileage of 25 mps. The residual of the model, for that specific observation, is 2 mpg.

Our example has 74 observations. Then, the model can predict one mpg for each car weight. Therefore, a dataset with 74 observations will have 74 residuals; one for each observation. 

Because $\hat{Y_n} = \hat{\beta_0} + \hat{\beta_1} x_n$, we can see that

$$
\begin{align}
e_n &= Y_n - \hat{Y_n} \\\\[10pt]
e_n &= Y_n - (\hat{\beta_0} + \hat{\beta_1} x_n)
\end{align}
$$

Yet, there is still another problem. We can still fit an infinite number of lines that will make the sumation of all the residuals equal to zero $(\sum^{74}_{n=1} e_n = 0)$ (residuals on one side of the real data cancel out with residuals on the other side of the real data). Minimizing the resiudals is not enough, as it will set an undefined problem.

To deal with this issue, OLS minimizes **squared** residuals. The OLS problem now becomes the following (where $\beta$ is a vector that contains $\beta_0$ and $\beta_1$):

$$
\operatorname*{min}_{\beta} \sum_n e_N^2 = \operatorname*{min}_{\beta} \sum_n (Y_n - (\hat{\beta_0} + \hat{\beta_1} x_n))^2
$$

Squaring the residuals have the following two attributes:

1. Allows to find a unique solution to the OLS problem.
2. It penalizes at a higher rate larger than smaller residuals.

### Algebraic solution
To find the $betas$ that minimize the sum of the squared residuals we proceed in a typical way:

1. Set the optimization problem.
2. Find the first order conditions (FOCs).
3. Solve the system of equations defined by the FOCs.
4. Confirm the silution is a minimum by checking the second order conditions (SOCs) (not included in this example)

**Step 1:** Set the optimization problem

$$ \operatorname*{min}_{\beta} \sum_n (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n)^2 $$

**Step 2:** Find the FOCs

$$
\begin{align}
FOC_0: \frac{\partial \sum e^2}{\partial \hat{\beta_0}} &= -2 \sum (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) = 0 \\\\[10pt]
FOC_1: \frac{\partial \sum e^2}{\partial \hat{\beta_1}} &= -2x_n \sum(Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) = 0
$$