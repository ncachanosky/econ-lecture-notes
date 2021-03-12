---
# Title, summary, and page position.
linktitle: "The Ramsey RESET Test"
weight: 4

# Page metadata.
title: The Ramsey RESET Test
type: book  # Do not modify.
---



---

## What are dummy variables

In some occasions it can be important to capture *categorical* (non-numerical) information. For instance, it may be of relevance to know the gender of an individual, or the race, or nationality, or any other categorial characteristic.

Even though these categories are not numbers, dummy variables allow the inclusion of this information in a regression by coding the categories into 1 (true) or zero (false).

Dummy variables work as switches, that move the fit of a regression from one category to the other. These switches can be in terms of (1) levels, (2) slopes, (3) both.

---

## The dummy trap

The dummy trap is the accidental creation of perfect multicollinearity. If there are $n$ categories, then the model can include up to $n-1$ dummy variables.

Assume a model that looks at the GDP per capita in each US State. The model consider the possibility that their of state-specific conditions that can affect the level of income per capita. All else equal, being in Colorado yields in average a different level of income than, say, Louisiana. The model needs to pick one state as reference, and then define 49 dummy variables, one per each state. 

A model that includes a dummy for all 50 states creates a perfect linear combination with the constant term. The constant is a column of ones. And because each dummy has 1 for each different states, the addition of all dummy variables produce the constant. If the model suffers from perfect multicollinearity, then the inverse the model cannot calculate the coefficients because the inverse $(X'X)^{-1}$ does not exist.

---

## Level and slope effects

### Level effect

A dummy variable can be used to change the **intercept** of the fitted line **without** changing the slope across different categories. For instance, you hypothesize that US states with high levels of oil production have higher levels of income per capita *all else equal*. A dummy with value 1 (true) for each state with high level of oil production *switches* between *low* and *high* level of income.

Consider the following model:

$$
y = \beta_0 + \beta_1 x + \gamma D + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    (\beta_0 + \gamma) + \beta_1 x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

Then, the intercept will be either $\beta_0$ or $\beta_0 + \gamma$ whether the dummy variable is 0 or 1.

### Slope effect

A dummy variable can also be used to change the **slope** of the fitted **without** changing the intercept line across different categories. This is done by interacting the dummy variable with the regressor you think has a different marginal effect across the different categories.

Consider the following model:

$$
y = \beta_0 + \beta_1 x + \gamma (xD) + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    \beta_0 + (\beta_1 + \gamma) x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

### Level and slope effect

Both, level and slope effect, can be included in a model. Combine both of the above examples.

$$
y = \beta_0 + \beta_1 x + \gamma_0 D + \gamma_1 (xD) + \varepsilon
$$

Because $D$ can be either 0 or 1:

$$
y =
\begin{cases}
    \beta_0 + \beta_1 x + \varepsilon            & \quad \text{if } D=0 \\\\
    (\beta_0 + \gamma_0) + (\beta_1 + \gamma_1) x + \varepsilon & \quad \text{if } D=1
\end{cases}
$$

Dummy effects in a graph

The plots below depict (1) level, (2) slope, and (3) the combined effects of a dummy variable in a regression. Plots are built with the following `STATA` code.

```
*==============================================================================*
* MODEL SPECIFICATION
* Create a model misspecification
* Code sample: 5.2
*==============================================================================*

*|CELL 1|----------------------------------------------------------------------*
*|Settings
set scheme s1color  // Set plot scheme

*|CELL 2|----------------------------------------------------------------------*
*|Create X-axis and dummy variables
drop _all
set obs 100

gen   X = _n
label variable X "X"
tsset X

gen     D = 1
label   variable D "dummy"

*|Create dummy effects
generate Y1 = 10 + 0.5*X
label variable Y1 "Y (without dummy)"
generate Y1_dots = .
replace  Y1_dots = 10 + 0.5*X + rnormal(0,2) in 1/20
replace  Y1_dots = 10 + 0.5*X + rnormal(0,2) in 60/80

generate Y2 = (10 + 20*D) + 0.5*X
label variable Y2 "Y (with intercept dummy)"
generate Y2_dots = .
replace  Y2_dots = (10 + 20*D) + 0.5*X + rnormal(0,2) in 21/45
replace  Y2_dots = (10 + 20*D) + 0.5*X + rnormal(0,2) in 81/100

generate Y3 = 10 + (0.5 + D)*X
label variable Y3 "Y (with slope dummy)"
generate Y3_dots = .
replace  Y3_dots = 10 + (0.5 + D)*X + rnormal(0,2) in 21/45
replace  Y3_dots = 10 + (0.5 + D)*X + rnormal(0,2) in 81/100

generate Y4 = (10 + 20*D) + (0.5 + D)*X
label variable Y4 "Y (with slope and intercept dummy)"
generate Y4_dots = .
replace  Y4_dots = (10 + 20*D) + (0.5 + D)*X + rnormal(0,2) in 21/45
replace  Y4_dots = (10 + 20*D) + (0.5 + D)*X + rnormal(0,2) in 81/100

*|Create plots: Level effect
twoway line Y1 Y2 X, ///
	   title("Dummy level (intercept) effect", size(small)) ///
	   lcolor(blue%75 green%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall) color(blue)) ///
	   text(30 -4 "{&beta}{sub:0}+{&gamma}", placement(w) size(vsmall) color(green)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size(vsmall) color(blue)) ///
	   text(53 50 "slope: {&beta}{sub:1}", placement(e) size(vsmall) color(green)) ///
	   legend(off) ///
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y2_dots X, mcolor(green%50) msize(vsmall)

*|Create plots: Slope effect
twoway line Y1 Y3 X, ///
	   title("Dummy marginal (slope) effect", size(small)) ///
	   lcolor(black%75 black%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size (vsmall) color(blue)) ///
	   text(83 50 "slope: {&beta}{sub:1} + {&gamma}", placement(e) size (vsmall) color(green)) ///
	   legend(off) ///
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y3_dots X, mcolor(green%50) msize(vsmall)
	   
*|Create plots: Level and slope effect
twoway line Y1 Y4 X, ///
	   title("Dummy level (intercept) and marginal (slope) effect", size(small)) ///
	   lcolor(blue%75 green%75) ///
	   xlabel(,labsize(vsmall)) ylabel(,labsize(vsmall)) ///
	   xtitle("X", size(vsmall))  ytitle("Y", size(vsmall)) ///
	   text(10 -4 "{&beta}{sub:0}", placement(w) size(vsmall) color(blue)) ///
	   text(30 -4 "{&beta}{sub:0}+{&gamma}", placement(w) size(vsmall) color(green)) ///
	   text(33 50 "slope: {&beta}{sub:1}", placement(e) size (vsmall) color(blue)) ///
	   text(103 50 "slope: {&beta}{sub:1} + {&gamma}", placement(e) size (vsmall) color(green)) ///
	   legend(off) ////
	 ||scatter Y1_dots X, mcolor(blue%50) msize(vsmall) ///
	 ||scatter Y4_dots X, mcolor(green%50) msize(vsmall) 
```


{{< figure library="true" src="econometrics/06_Specification/Fig_02.png" >}}


{{< figure library="true" src="econometrics/06_Specification/Fig_03.png" >}}


{{< figure library="true" src="econometrics/06_Specification/Fig_04.png" >}}

---

## Example: The Gender Wage Gap

Consider the issue of the *gender wage gap* as an example. Let's say the working population is separated between `males` and `females`. Then, a dummy variable $D$ will take a value of 1 if the person is male (female) and a value of 0 is the person is (female) male. It does not matter which category gets the 1 and which category gets the 0. It just a matter of consistently interpreting the results. Say $D$ is 0 if the person is `male` and 1 if the person is `female`. Then, a regression looking at wages would show the relative impact of female wages with respect to men. This is, for instance, the way in which the *gender wage gap* is presented.

