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
---

## Example: The Gender Wage Gap

Consider the issue of the *gender wage gap* as an example. Let's say the working population is separated between `males` and `females`. Then, a dummy variable $D$ will take a value of 1 if the person is male (female) and a value of 0 is the person is (female) male. It does not matter which category gets the 1 and which category gets the 0. It just a matter of consistently interpreting the results. Say $D$ is 0 if the person is `male` and 1 if the person is `female`. Then, a regression looking at wages would show the relative impact of female wages with respect to men. This is, for instance, the way in which the *gender wage gap* is presented.

