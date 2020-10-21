---
# Title, summary, and page position.
linktitle: "Introduction to Econometrics"
weight: 1

# Page metadata.
title: Introduction to Econometrics
date: "2018-09-09T00:00:00Z"
type: book  # Do not modify.
---



---
# What is econometrics?
It is easy to infer a definition of [**econometrics**](https://en.wikipedia.org/wiki/Econometrics) from its etymology. The literal interpretation of the word *econometrics* is *economic measurement*. More precisely, econometrics is the application of statistical techniques to economics.

Econometrics is not in itself economic theory. It is, however, one of its complements. Economic theory estipulates *qualitative* relationships. For instance, a demand function can be represented as $Q^D = a - bp$; where $Q^D$ is the quantity demanded, $p$ is the price of the good in question, and $a$ and $b$ are two parameters. From economic **theory** we know that $a$ and $b$ are positive $(a, b, >0)$. However, economic theory **does not** give values to either $a$ or $b$. We do not know, just from theory, how steep the demand line is. Econometrics is a method through which the values of $a$ and $b$ are estimated. If economic theory is **qualitative**, then econometrics is **quantitative**.

Note that econometrics uses the values of **observable** economic **variables** (such as quantities and prices) to estimate what would be the **parameters** in an economic model (such as $a$ and $b$ in the demand function). This is a different excercise from finding, say, an $x^*$ that optimizes the value of $y = f(x)$ with **given** parameter values.


---
# Uses of econometrics
Because econometrics itself is a method to measure economic parameters, it can be used in different ways such as:

* To test an hypothesis
* To make an economic description
* To forecast or predict the unobserved value of economic variables

For instance, you may want to test the hunch or intuition (the hypothesis) that the point-elasiticy of the demand function equals 1 at a given price.[^1] Alternatively, you may just be interested in what the slope of the demand is at a given price range, so that you can plan your business strategy accordingly. Finally, you may want to estimate what the quantity demanded of a gadget you produce would be in a country where you do not operate by looking at data from countries where you do have business operations.

These are three very distinctive uses of econometrics. These different uses also shows that econometrics, and doing empirical work, is not just about testing hypothesis. Furthermore, this also means that, epistemologically speaking, doing econometrics and empirical work does not mean one is necessarily being a logical positivist (later known as [logical empiricism](https://plato.stanford.edu/entries/logical-empiricism/)).


---
# The econometric technique
## Regression analysis and the estimation rule
There are different ways to estimate the value of a parameter, such as the slope of a demand function. One alternative is to ask your mother what value she thinks the slope has. This is an easy method, but also very likely to be very innacurate. Econometrics applies regression analysis to infer a more accurate estimation of these parameters. 

The estimation of the slope of a demand function makes use (ideally) of a large set of price and quantities. All these prices and quantities do not offer a perfect match to one and unique slope of the demand function. Therefore, we need a rule to decide how the slope must be estimated. The econometric technique is mostly built to minimize errors between what the econometric model estimates and the observed data.

### Example
Let the quantity demanded of a good $(Q^D)$ depend on its price $p$, the price of a substitute good $p_S$, and the level of disposable income of potential customers $Y_D$. Then, we can represnet this relationship in the following way

$$ Q^D = \beta_0 + \beta_1 P + \beta_2 P_S + \beta_3 Y_D + \epsilon $$

Through data collection (observation) we know values of $Q^D$, $P$, $P_S$, and $Y_D$. The betas $(\beta_1, ..., \beta_3)$ represent the marginal effects of each variable has on $Q^D$. We also know that our observations are going to be imperfect and, therefore, there is some *error* $(\epsilon)$ between our observed data and $Q^D$. As will be clear later, regressions typically have a constant term $(\beta_0)$.

After applying a regression analysis we get an estimation of the parameters, that is, the betas. Our estimated model may look the following way (where the *hats* denote estimated values):

$$ \hat{Q^D} = \hat{\beta_0} + \hat{\beta_1} P + \hat{\beta_2} P_S + \hat{\beta_3} Y_D $$

$$ \hat{Q^D} = 25 - 0.25 P + 0.15 P_S + 0.10 Y_D $$

At this point is enough to point to two issues. The first one is that there is *hat* on top of $Q^D$. This means that once you have your beta estimations,you can use the prices and disposable income informatio to *predict* or *estimate* values of $Q^D$. The second one is that there is no error term. The error term, which is unobservable, is estimated by the *residual* $(e)$, which will be the difference between the real and observed $Q^D$ and the model estimation $\hat{Q^D}$: $e = Q^D - \hat{Q^D}$.

Now, some terminology. The left-hand variable $(Q^D)$ is called the dependent variable. The right-hand variables are called the **regressors** (what would be the *independent* variables).

{{% callout warning %}}
In econometrics, the word **explanation** means that a change of a variable is correlated ("explains") part of the change of the dependent variable.

In econometrics, the word **explanation** does not have a *cause-effect* meaning: It does not mean that a change of a regressor is the cause of a change in the dependent variable

{{% /callout %}}

---
## Types of datasets
What type of econometric techniques can be used depends on the type of data at your disposal. There are three types of datasets:

1. Cross-sectional
2. Time-series
3. Panel data (also known as longitudinal data)

**Cross-sectional** data is the case when the data includes a number of *sections* with data for one time-period only. For instance, income and unemlpoyment informatio for the 50 U.S. states for the year 1930.

**Time-series** data is the inverse situation. The dataset has information of one section for a number of years. For instance, the unemployment rate of the state of Colorado between 1920 and 1950.

**Panel data** is the combination of the other two. Now the dataset includes information for more than one section and more than one time period. For instance, income for the 50 U.S. states between 1920 and 1950.


---
## A recommendation and a word of advice
Before delving into the details of econometric analysis, a recommednation and a word of advice

### A recommendation: Think of econometrics more as an art more than as hard-science
Econometrics can be highly technical and theoretical. There is a reason why econometrics has the fame of being a difficulty subject. However, econometrics is the applciation of **statistical** methods. This has two important implications.

First, there is no unique answer to the question of what value is the right estimation of your unknown parameters. This means that differnet people will disagree on what the right approach should be. And in many times there is no definite way to sort out those disagreements.

Second, there is no unique method or *model specification* that can be used to make an estimation. Several regression analyses may be possible. Again, different people can disagreee on what the best application is, without a definite way to sort out the difference of opinion.

These implications mean that, even if an estimatino is obtained following strict and precise theoretical methods, the estimation output is open to interpretation. While regression analysis can be obkective, in the sense of following a specific methods and thoeries, model applicaiton and interpretation is subjective. How to apply and read a model requires the economist intuition of what is happening behind the scences (unobservable) and what the proper reading of the outout should be.

Therefore, econometrics is not only a scientific application, it also an **art**, in the sense that each econometric application is driven by a subjective point of view that can vary from person to person.

### A word of advice: Do not confuse econometrics with economics
Even thouth econometrics is an important field in economics, neither econometrics is economics nor economics is econometrics. 

Anyone can be an excellent economisit and at the same time have a very limited knowledge of econometrics. In fact, some of the most influential scholars such as [James M. Buchanan](https://en.wikipedia.org/wiki/James_M._Buchanan[), [Ronald H. Coase](https://en.wikipedia.org/wiki/Ronald_Coase), or [Friedrich A. von Hayek](https://en.wikipedia.org/wiki/Friedrich_Hayek) made little of use intense mathematics or econometric applications.

Inversely, someone can be an outstanding econometrician while being clueless about economics. Economics is way of thinking (theory) about how the world looks. Economics itself is not a way of testing an hypothesis. Statistics without a theory is not economics, it is just statistics. To wit, [economics is not statistics (and vice versa)](https://www.peterleeson.com/Economics_is_Not_Statistics.pdf).



<!-- FOOTNOTES -->
[^1]: Recall that the point price-elasticity of demand is: $|\epsilon| = \frac{\partial Q^D}{\partial p} \cdot \frac{p}{Q^D}.$
