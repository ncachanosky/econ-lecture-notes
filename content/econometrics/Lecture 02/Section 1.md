---
# Title, summary, and page position.
linktitle: "Univariate regressions"
weight: 1

# Page metadata.
title: Univariate regressions
type: book  # Do not modify.
---

---
## What is Ordinary Least Squares (OLS)?
[OLS](https://en.wikipedia.org/wiki/Ordinary_least_squares) is the most common method to estimate the *parameters* of a linear regression such that the sum of the **squared errors** is minimized. In more general terms, OLS is one application of a group of *linear least squares* methods.

Assume we want to estimate the linear relationship between mileage (mpg) $(Y)$ of autombiles with respect to its weight $(x)$. The dependent variable is $Y$ and $x$ is the regressor. Then, we are assuming that $Y$ has a linear relationship with respect to its weight.

Let $i = 1,...,N$ be the number of observations; that is, how many mileage and weight observations we have at our disposal. The theoretical representation of this relationship is the following:

$$
\begin{align}
mpg_n &= \beta_0 + \beta_1 weight_i + \varepsilon_i \\\\[10pt]
Y_n   &= \beta_0 + \beta_1 x_i + \varepsilon_i
\end{align}
$$

The error term $(\varepsilon)$ is capturing random situations that would affect the mileage of the car, such as weather conditions, average speed of the driver, or altitude. The error term is purely random and captures the variations of $Y$ that cannot be explained by $x$. We can then split an econometric regression in two parts. A deterministic component (the constant plus the regressors) and a stochastic component (the error term). Because $Y$ is modeled as a function of a deterministic and a random variable, $Y$ is also a random variable $Y = f(x, e)$. There is an assymmetry in how variables are treated; while the dependent variable is assumed to be *stochastic*, the regressors are assumed to be *deterministic*.[^1]

We can also see that $\beta_1$ is the **marginal effect** of $x$ on $Y$: $\frac{\partial Y}{\partial x} = \beta_1$.

Let's use the 1978 automobile dataset in `STATA`. The code blow produces a [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) between mileage (mpg) and weight (lbs.) The dataset has 74 observations, therefore the scatter plot will have 74 points (mileage-weight relationships).


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

We can draw an infinite number of lines that go through the scatter plot. But, we are not looking for *any* line, we are looking for the line that would minimize errors between a predicted mileage and the observed mileage when looking at the weight ofa car. OLS is a method to find such line. 

---
## The OLS method
### What is OLS doing?
We need to find the values of $\beta_0$ and $\beta_1$ that would minimize prediction mistakes. Once we have estimated values for our $betas$, we can use the $weight$ data to predict $mileage$ with the smaller errors possible. The following equation shows the notation of the econometric model using the estimated parameter to predict values of the dependent variables.

$$ \hat{Y_i} = \hat{\beta_0} + \hat{\beta_1} x_i $$

Before proceeding, is important to distinguish betweeen the **error (or disturbance)** term $(\varepsilon)$ and the **residual** $(e).$


{{% callout warning %}}
Do not confuse the [**error term** with the **residual**](https://en.wikipedia.org/wiki/Errors_and_residuals).

---
**The error $(\varepsilon)$ term**  
The *error* is the difference between the **conditional expected** value of the dependent variable $(E[Y|x])$ and a random observation taken from the sample: $\varepsilon_i = E[Y|x_i] - Y_i$. If the mean mileage of a car with a weight of 2000 pounds is 27 mpg and a randomly observed car has an mpg of 25, then the error is 2 mpg. A regression assumes these errors are random. The error captures random effects that make the dependent variable deviate from its mean (for instance random measurement errors).

**The residual $(e)$**  
The residual (or fitting deviation) is the difference between the conditional mean of the dependent variable $(E[Y|x])$ and the predicted value $(\hat{Y})$: $e_i = E[Y|x] - \hat{Y_i}$. In other words, the residual is the difference between the observed data (sample) and the model predictions. In this sense. the *residual* is like a *proxy* of the unovserbable *error*.
{{% /callout %}}

Our example has 74 observations. Because the model can predict one $mpg$ for each car $weight$, there is one *residual* for each observation. Because $\hat{Y_i} = \hat{\beta_0} + \hat{\beta_1} x_i$, we can see that

$$
\begin{align}
e_i &= Y_i - \hat{Y_i} \\\\[10pt]
e_i &= Y_i - (\hat{\beta_0} + \hat{\beta_1} x_i)
\end{align}
$$

Yet, there is still a situation that requires a solution. We can fit an infinite number of lines that will make the sumation of all the *residuals* equal to zero $(\sum^{74}_{i=1} e_i = 0)$ (residuals cancel out)). Canceling the residuals is not enough because only one of those infinite lines is the one we are looking for. To find the line we are looking for OLS minimizes the **squared** residuals. We can now state the OLS problem in more precise terms:

$$
\operatorname*{min}_{\beta_{1,2}} \sum_i e_i^2 = \operatorname*{min}_{\beta} \sum_n (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i)^2
$$

Squaring the residuals has the following two attributes:

1. Allows to find a unique solution to the OLS problem.
2. It penalizes at a higher rate larger than smaller residuals.

The OLS estimation fits the *best* line through the points in the scatter plot. Where *best* is defined as minimizins the squared residuals constrained on the prediction being a straight line. The following `STATA` code adds the regression result to the scatter plot.

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific  // Set plot scheme
sysuse auto  // Load 1978 Automobile Data from STATA

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

The dashed line plots the fitted line, that is, all the $\hat{Y}$ values estimated by the regression. This line can be interpreted as the expected value of $Y$ conditional on a given value of $x$. Because $e$ is random, $E[Y|x] = \hat{Y}$.

We can use the same dataset to illustrate the importance of having a large and representative sample. The `STATA` code below creates two random subsamples with half observations each. The figure shows how different samples of the same populatoin can lead to different regression results (because the code uses random values, your own results will not coincide with the ones below)

```stata
*==============================================================================*
* ORDINARLY LEAST SQUARES
* Univariate regression
* Code sample: 2.3
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings and required data
set scheme scientific  // Set plot scheme
sysuse auto  // Load 1978 Automobile Data from STATA

*|CELL 2|----------------------------------------------------------------------*
*|Sort the dataset randomly
generate random = runiform()
sort random

generate id = _n <= 74/2

*|CELL 3|----------------------------------------------------------------------*
*|Build scatter plots
twoway scatter mpg weight if id==0, ///
	   mcolor(red%50) ///
	   xlabel(2000(500)5000) ///
	   ylabel(10(5)40) ///
	   xlabel(, grid labsize(small)) xtitle(, size(small)) ///
	   ylabel(, grid labsize(small)) ytitle(, size(small)) ///
	 ||lfit mpg weight if id==0, ///
	   lcolor(red%50) ///
	 ||scatter mpg weight if id==1, ///
	   mcolor(green%50) msymbol(O) ///
	 ||lfit mpg weight if id==1, ///
	   lcolor(green%50) ///
	   legend(off)
	   
*==============================================================================*
*|THE END|=====================================================================*
*==============================================================================*
```

{{< figure library="true" src="econometrics/lecture 02/Fig 2.03.png" numbered="true" title=" Scatter plot: Mileage versus Weight">}}  

### Algebraic solution
To find the $betas$ that minimize the sum of the squared residuals we proceed in a typical way:

1. Set the optimization problem.
2. Find the first order conditions (FOCs).
3. Solve the system of equations defined by the FOCs.
4. Confirm the silution is a minimum by checking the second order conditions (SOCs) (not included in this example)

**Step 1:** Set the optimization problem
$$ \operatorname*{min}_{{\beta}} \sum_i (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i)^2 $$

**Step 2:** Find the FOCs
$$
\begin{align}
FOC_0: \frac{\partial \sum e^2}{\partial \hat{\beta_0}} &= -2 \sum (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i) = 0 \\\\[10pt]
FOC_1: \frac{\partial \sum e^2}{\partial \hat{\beta_1}} &= -2 \sum(Y_i - \hat{\beta_0} - \hat{\beta_1} x_i) x_i = 0
\end{align}
$$

Note that the FOCs imply that the solution will also make the residuals cancel out $(\sum e = 0)$ (the term in parenthesis is $e$).

**Part 3:** Solve the system of equations defined by the FOCs.  
Get $\hat{\beta_0}$ from the first equation. Use the following property: $\sum x = N\bar{x}$ where $\bar{x} = \frac{1}{N} \sum x$.

$$
\begin{align}
-2 \sum (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i) &= 0 \\\\[10pt]
\sum (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i) &= 0 \\\\[10pt]
N \bar{Y} - N \hat{\beta_0} - \hat{\beta_1} N \bar{x} &= 0 \\\\[10pt]
\hat{\beta_0} &= \bar{Y} - \hat{\beta_1} \bar{x}
\end{align}
$$

Replace now $\hat{\beta_0}$ into the second equation.

$$
\begin{align}
-2 \sum (Y_i - \hat{\beta_0} - \hat{\beta_1} x_i) x_i &= 0 \\\\[10pt]
\sum (Y_i - \bar{Y} + \hat{\beta_1} \bar{x} - \hat{\beta_1} x_i) x_i &=0 \\\\[10pt]
\sum Y_i x_i - \sum \bar{Y} x_i + \hat{\beta_1} \sum \bar{x} x_i - \hat{\beta_1} \sum x_i^2 &=0 \\\\[10pt]
\sum Y_i x_i - \sum \bar{Y} x_i + \hat{\beta_1} \left( \bar{x} x_i - \sum x_i^2 \right) &=0 \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_i x_i - \sum \bar{Y} x_i}{\sum x_i^2 - \sum \bar{x} x_i} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_i x_i - \bar{Y} \sum x_i}{\sum x_i^2 - \bar{x} \sum x_i} \\\\[10pt]
\hat{\beta_1} &= \frac{\sum Y_i x_i - N \bar{Y} \bar{x}}{\sum x_i^2 - N \bar{x}^2} \\\\[10pt]
\hat{\beta_1}^* &= \frac{\sum (x_i - \bar{x})(Y_i - \bar{Y})}{\sum (x_i - \bar{x})^*}
\end{align}
$$

Now use the value of $\hat{\beta_1}$ to get the value of $\hat{\beta_0}$:

$$ \hat{\beta_{0}^{*}} = \bar{Y} - \hat{\beta_{1}^{*}} \bar{x} $$

If we now replace $\hat{\beta_0}$ into the equation, we can express $\hat{Y}$ as deviations from its mean when $x_i$ deviates from its own mean:

$$
\begin{align}
\hat{Y}_i &= \hat{\beta_0} + \hat{\beta_1} x_i \\\\[10pt]
\hat{Y}_i &= \left( \bar{Y} - \hat{\beta_1} \bar{x} \right) + \hat{\beta_1} x_i \\\\[10pt]
\hat{Y}_i &= \bar{Y} + \hat{\beta_1} (x_i - \bar{x})
\end{align}
$$

This method has the following properties.:

1. Minimizes the squared residuals $(\sum e_n^2)$
1. Makes all residuals cancel out $(\sum e = 0)$
1. The fitted line passes through the sample means $(\bar{Y}, \bar{x})$.
1. The mean value of $Y$ equals the mean value of $\hat{Y}$ (because $\sum (x_i - \bar{x}) =0$).

There is one more lesson to get from this excercise. As you can probably imagine, finding the optimal $betas$ can become increasingly complicated very fast as we add more regressors to the model. Matrix algebra (very common in econometrics) can make the mathematics of econometrics much simpler. An example of this simpler approach is included in the next section, where we solve the same problem for a regression with multiple regressors. 

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/lecture 02/OLS (simple example).xlsx" %}}Download OLS simple example.{{% /staticref %}}


---
## How useful are univariate regressions?
Using a single regressor has very limited *practical* applications. Most regressions use several regressors to (1) achieve a better estimation and (2) obtain a more accurate intepretation of the $betas$. 

However, a univariate regression is very useful *pedagogically* because it offers a simple way to understand what a statistical software is doing behind the scenes when you run a regression. The most important lesson of this section is to understand what OLS is doing, and how is it doing it.



<!-- FOOTNOTES -->
[^1]: Of course, the regressors may also be stochastic variables. However, a regression **assumes** they are deterministic. 