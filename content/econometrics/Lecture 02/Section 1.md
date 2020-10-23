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

Let $n = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following:

$$
\begin{align}
mpg_n &= \beta_0 + \beta_1 weight_n + \varepsilon_n \\\\[10pt]
Y_n   &= \beta_0 + \beta_1 x_n + \varepsilon_n
\end{align}
$$

The error term $(\varepsilon)$ is capturing random situations that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude.

Let's use the 1978 automobile dataset in `STATA` and run a [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) between mileage and weight. The following `STATA` code will produce the scatter plot shown below ([Figure 1](#figure--scatter-plot-mileage-versus-weight)). The dataset has 74 observations, therefore the scatter plot will have 74 points (mileage-weight relationships).


```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.1
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific  // Set plot scheme
sysuse auto  // Load 1978 Automobile Data from STATA

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

{{< figure library="true" src="econometrics/lecture 02/Fig 2.01.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  

We can draw an infinite number of lines that go through the scatter plot. But, we are not looking for *any* line, we are looking for the line that would minimize errors of the prediction of mileage when looking at the weight of a car. OLS is a method to find such line. 

---
## The OLS method
### What is OLS doing?
We need to find the values of $\beta_0$ and $\beta_1$ that would minimize estimation mistakes. Once we have estimated values for our $betas$, we can use the $weight$ data to predict $mileage$ with the smaller errors possible. The estimated $betas, (\hat{\beta_0}, \hat{\beta_1})$, can be used to estimate $mileage, (\hat{Y_n})$ for each $weight (x_n)$.

$$ \hat{Y_n} = \hat{\beta_0} + \hat{\beta_1} x_n $$

{{% callout warning %}}
Do not confuse the **error** term with the **residual**.
{{% /callout %}}

> Before proceeding, is important to distinguish betweeen the **error** term $(\varepsilon)$ and the **residual** $(e).$ The *error* captures the random events that produce a difference between weight and mileage. Because this is a random variable (for instance changes in weather) the error is also referred as the **stochastic error** term. The error is unobservable. If all these random events were known, then we would be able to add them to the model. The *residual* term is the difference between the model prediction and the real world data (the residue that the model fails to explain). In this sense. the *residual* is like a *proxy* of the unovserbable *error*. Because the *error* is unobservable, OLS minimizes the *residual*.

More precisely, the residual equals: $e_n = Y_n - \hat{Y_n}$. For instance, after you estimate the $betas$ of the equation, a weight of 2000 pounds predicts a mileage of 27 mpg. However, you know that a car with a weight of 2000 pounds has a mileage of 25 mps. The residual of the model, for that specific observation, is 2 mpg.

Our example has 74 observations. Because the model can predict one $mpg$ for each car $weight$, there is one *residual* for each observation. Because $\hat{Y_n} = \hat{\beta_0} + \hat{\beta_1} x_n$, we can see that

$$
\begin{align}
e_n &= Y_n - \hat{Y_n} \\\\[10pt]
e_n &= Y_n - (\hat{\beta_0} + \hat{\beta_1} x_n)
\end{align}
$$

Yet, there is still a situation that requires a solution. We can fit an infinite number of lines that will make the sumation of all the residuals equal to zero $(\sum^{74}_{n=1} e_n = 0)$ (residuals cancel out)). Canceling the residuals is not enough because only one of those infinite lines is the one we are looking for. To deal with this issue, OLS minimizes **squared** residuals. The OLS problem now becomes the following:

$$
\operatorname*{min}_{\beta_{1,2}} \sum_n e_N^2 = \operatorname*{min}_{\beta} \sum_n (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n)^2
$$

Squaring the residuals has the following two attributes:

1. Allows to find a unique solution to the OLS problem.
2. It penalizes at a higher rate larger than smaller residuals.

The OLS estimation fits the *best* line through the points in the scatter plot. Where *best* is defined as minimizins the squared residuals constrained on the prediction being a straight line. We can see the result below and then proceed to discuss the mathematical estimation technique in more detail.

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific	// Set plot scheme
sysuse auto				// Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight, ///
	   mcolor(blue%50) ///
	   xlabel(2000(500)5000) ///
	   ylabel(10(5)40) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small)) || ///
	   lfit mpg weight, ///
	   lcolor(black) ///
	   legend(position(6) rows(1) size(vsmall))
	   
*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/lecture 02/Fig 2.02.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  

### Algebraic solution
To find the $betas$ that minimize the sum of the squared residuals we proceed in a typical way:

1. Set the optimization problem.
2. Find the first order conditions (FOCs).
3. Solve the system of equations defined by the FOCs.
4. Confirm the silution is a minimum by checking the second order conditions (SOCs) (not included in this example)

**Step 1:** Set the optimization problem
$$ \operatorname*{min}_{{\beta}} \sum_n (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n)^2 $$

**Step 2:** Find the FOCs
$$
\begin{align}
FOC_0: \frac{\partial \sum e^2}{\partial \hat{\beta_0}} &= -2 \sum (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) = 0 \\\\[10pt]
FOC_1: \frac{\partial \sum e^2}{\partial \hat{\beta_1}} &= -2 \sum(Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) x_n = 0
\end{align}
$$

Note that the FOCs imply that the solution will also make the residuals cancel out $(\sum e = 0)$ (the term in parenthesis is $e$).

**Part 3:** Solve the system of equations defined by the FOCs.  
Get $\hat{\beta_0}$ from the first equation. Use the following property: $\sum x = N\bar{x}$ where $\bar{x} = \frac{1}{N} \sum x$.

$$
\begin{align}
-2 \sum (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) &= 0 \\\\[10pt]
\sum (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) &= 0 \\\\[10pt]
N \bar{Y} - N \hat{\beta_0} - \hat{\beta_1} N \bar{x} &= 0 \\\\[10pt]
\hat{\beta_0} &= \bar{Y} - \hat{\beta_1} \bar{x}
\end{align}
$$

Replace now $\hat{\beta_0}$ into the second equation.

$$
\begin{align}
-2 \sum (Y_n - \hat{\beta_0} - \hat{\beta_1} x_n) x_n &= 0 \\\\[10pt]
\sum (Y_n - \bar{Y} + \hat{\beta_1} \bar{x} - \hat{\beta_1} x_n) x_n &=0 \\\\[10pt]
\sum Y_n x_n - \sum \bar{Y} x_n + \hat{\beta_1} \sum \bar{x} x_n - \hat{\beta_1} \sum x_n^2 &=0 \\\\[10pt]
\sum Y_n x_n - \sum \bar{Y} x_n + \hat{\beta_1} \left( \bar{x} x_n - \sum x_n^2 \right) &=0 \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_n x_n - \sum \bar{Y} x_n}{\sum x_n^2 - \sum \bar{x} x_n} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_n x_n - \bar{Y} \sum x_n}{\sum x_n^2 - \bar{x} \sum x_n} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_n x_n - N \bar{Y} \bar{x}}{\sum x_n^2 - N \bar{x}^2} \\\\[10pt]
\hat{\beta_1}^* &= \frac{\sum (x_n - \bar{x})(Y_n - \bar{Y})}{\sum (x_n - \bar{x})^*}
\end{align}
$$

Now use the value of $\hat{\beta_1}$ to get the value of $\hat{\beta_0}$:

$$ \hat{\beta_{0}^{*}} = \bar{Y} - \hat{\beta_{1}^{*}} \bar{x} $$

This method achieves the following two objectives:

1. Minimize the squared residuals $(\sum e_n^2)$
2. Make all residuals cancel out $(\sum e = 0)$

There is one more lesson to get from this excercise. As you can probably imagine, finding the optimal $betas$ can become increasingly complicated very fast as we add more regressors to the model. Matrix algebra (very common in econometrics) can make the mathematics of econometrics much simpler. An example of this simpler approach is included in the next section, where we solve the same problem for a regression with multiple regressors. 

{{<icon name="file-download" pack="fas" >}} [Download simple OLS example](static/media/econometrics/lecture 02/OLS (simple example).xlsx)


{{% staticref "media/econometrics/lecture 02/OLS (simple example).xlsx" %}}Download Excel file with example.{{% /staticref %}}


static\media\econometrics\lecture 02\OLS (simple example).xlsx

## How useful are univariate regressions?