---
# Title, summary, and page position.
linktitle: "Running your first regression"
weight: 4

# Page metadata.
title: Running your first regression
type: book  # Do not modify.
---

---

This section walks you through running your first regression. There are two issues pay attention to in this exercise. One is the *technical* discussion of how to run a regression and how to read the results we studied in the previous sections. The other one is to pay attention to *subjective* interpretation of how a model should be built and what results may be saying to us. A discussion and interpretation of a regression results is part of the econometric exercise as well.

The exercise follows the following steps:

1. Organize and clean your data
2. Familiarize yourself with your data
3. Define your models
4. Run your regressions
5. Evaluate the quality of the models

---

## Organize and clean your data

Consider first **how** is your data stored. If you are working with `STATA`, or any other statistical package, you may be lucky and have access to the data in your software format. All you need to is load the file to your software. For instance, STATA data files have the `.dta` extension.

However, it is possible that data stored in a more general format, just as `.csv` or Excel file. It is also possible that you will have to build your dataset before *importing* into your statistical software.

Unless the data you need is already in a dataset (of one format or another, you will have to create your own dataset. If that is the case, you may want to consider *how* you order your data.

Let us use an hypothetical example to show how you can organize your dataset to make it easy to read and explore. Assume you are looking at data for the 50 U.S. states.

Data is usually organized the following way. Regressors are columns and rows are observations. In addition, you know you have three types of variables: (1) the **dependent** variable $(y)$, (2) your regressors **of interest** $(x_i)$, (3) and our **control** variables $(z_j)$. Then, you can start with some metadata such as the observation number and the U.S. state. Each row is one observation (or one state). This metadata helps to identify each row. Then you can identify (with borders or different colors) your dependent variable. To the right you can have your variable(s) of interest. Finally, the last set of columns can be your control variables. You may also want to consider other *format* edits that will facilitate your reading of the data such as number of decimals, or horizontal lines every a few observations, and so on).

The figure below is an example of how a user-friendly dataset in Excel may look like.

{{< figure library="true" src="econometrics/03_OLS/Fig_09.png" >}}

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/03_OLS/Dataset format example.xlsx" %}}Download Excel sample file.{{% /staticref %}}

A user-friendly format of your dataset is important because you may need to do some data exploration at some point in your regression exercise. Maybe you need to clean up some typos, or identify outliers and missing values. And if you want to go back to the original file, then you want the information in that file as easy to read and navigate as possible. It is also a good gesture towards third-parties using your dataset as well. 

Besides a thinking of format that would facilitate the visual navigation of the file, you also want to think what format can produce errors when importing an `Excel` or `.csv` file into your statistical software. You will learn this with experience and use of your statistical software of choice. Just to give a couple of examples. If the first column has the regressor's names, then you may need to avoid `spaces` and resort to `underscores` (for instance, `Variable_1` instead of `Variable 1`). Another potential issue may the use of thousand delimiter (use `10000` instead of `10,000`).

The following `STATA` code produces all the output shared below.

---

## Familiarize your self with the data

Let us use the *auto* dataset in `STATA` and assume we want to study the price of cars $(y)$ as a function of mileage (mpg) $(x)$. For this, we have a dataset with a number of variables. Our first step, once we have data ready to use, it so familiarize with the information.

A good econometric analysis usually requires knowledge of how the data looks, what are the correlations, where are there any missing values, and so on. 

### Statistical summary

Statistical summaries are a first approach to see how your data looks like. This is particularly useful in very large datasets where a detailed view of the whole information may not be feasible.

The following table provides the number of available observations for each regressor (each column), the mean, standard deviation, and minimum and maximum values.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 01.png" >}}

Recall that an econometric regression *explains* variations. That is, how much of the variations of $y$ around its mean can be explained by variations of the regressors $(x_i)$ around their means. A regressor with low standard deviation (in relation to the mean) suggests that such variable may not have explanatory power (is similar to a constant, it does not vary). On the other hand, a dependent variable with a low standard deviation (in relation to its mean) suggests that there is not much to *explain* in that variable.

### Correlation matrix

A summary statistics table provides some information about each variable, but does not provide information of how are they related. Our next step is to look at the correlation matrix of all the variables.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 02.png" >}}

Looks like `weight` and `length` are the two variables more positively correlated with your dependent variable, `price`. For some reason, seems that the higher `mileage` (mpg) the lower the price, when in principle we would expect the opposite (can you think of a reason)? But, we should not jump to conclusions because it is also the case that `mileage` is highly negatively correlated with `weight` and `length`. We need a full regression to estimate the marginal and controlled effect of `mileage` on the `price` of the cars.

A correlation matrix is a first look at which variables have a positive or negative relationship and how strong is that relationship.

### Scatter plots

After looking at the correlation matrix, you suspect that `weight` and `legnth` may be good candidates for your regression. These are likely to be good control variables because the `mileage` of a car is not independent of its `weight` or `length`. Let's look, then, at three scatter plots, one for each regressor with respect to the dependent variable.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 03.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 04.png" >}}

{{< figure library="true" src="econometrics/03_OLS/OLS Example 05.png" >}}

The scatter plots reflect the negative and positive slopes you saw in the correlation matrix. Look at the first plot, where there seems to be an [outlier](https://en.wikipedia.org/wiki/Outlier). Is that point accurate or is there a typo in your source? If the data is correct, then you need to decide if you want to keep it your regression or not. The answer that questions depends on what information you want from your regression. You want to capture the relatonship of the whole sample or you want an estimation of the relationship of *normal* (average) cars?

Look now at the second and third scatter plots. You can see that to the left side of the graph, dots are closer to the fitted line than dots to the right side of the graph. We will get back to this issue in a later chapter. But, the looks of these scatter plots suggest that, for `weight` and `length` the accuracy of the model prediction is not even. A univariate model would be more accurate for lighter and shorter cars than would be for heavier and longer cars.  

---

## Define and run your models

Having now an impression of how data looks like, we can develop our regression models. Remember our objective, to find the relationship between `price` and `mileage`. We know, however, that we also need control variables if we want to obtain an unbiased estimation.

For this purpose, we are going to build a base model and then run different versions of the model for **robustness checking**. Remember that every regressor we add to the model brings information but consumes a degree of freedom. Therefore, we can specify different models with different regressors and see if, all of them, provide more or less similar results.

The relevant question is what other variables have an effect on the `price` of cars besides its `mileage`. It seems that all our regressors can contribute to explain car prices. `Mileage` is important, but so is the car' (1) weight, (2) length, (3) how many repairs it had since 1978, (4) its headroom, and (5) the trunk size.

Our base model, then, has a total of one variable of interest $(x)$ and 5 control variables ($z_1, ..., z_5)$:

$$
y_i = \beta_0 + \beta_1 x_i + \gamma_1 z_{1,i} + \gamma_2 z_{2,i} + \gamma_3 z_{3,i} + \gamma_4 z_{4,1} + \gamma_5 z_{5,1} + \varepsilon_i
$$

Before discussing different versions of the base model, let us run this regression in `STATA` and see what output we get. There is plenty of information here, and we are still not able to read all of it. But, we can start by learning how to read what we learn so far in a typical regression output.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 06.png" >}}

The estimation of the model is in the second table. The header's row shows `price` as the dependent variable. The regressors are located below (in the same order used in the code) with the constant (`_const`) at the end. The second row shows the $betas$. In this model, for instance, a change of one unit in the `mileage` (mpg) explains, **in average**, a fall of 101.4388 units in the `price` variable. We will discuss how to read the other columns to the right as we move through the next chapters. The coefficients of the output say our base model looks the following way (allowing for rounding):

$$
\hat{y_i} = 12,266 - 101.44 x_i + 4.95 z_{1,i} - 112.41 z_{2,i} + 889.67 z_{3,1} - 652.13 z_{4,i} + 80.29 z_{5,i}
$$

We can now look at the data above the coefficient's table. The first information that appears to the left is the [partition of sum of squares](https://econ-lecture-notes.netlify.app/econometrics/03_ols/section-3/#partition-of-sum-of-squares). We have $ESS$ (model), $RSS$ (residual), and $TSS$ (total) respectively. You can see that $model + residual = total$. 

On the right side there is some regression evaluation information. You have the total number of observations $(N=69$), the $R^2$, the $\bar{R}^2$, and the $RMSE$. You can see that $R^2 = \frac{model}{total}$. Finally, note that $\bar{R}^2 < R^2$.

We do not know, yet, if our base model is the best one. We need to look at the output, data information, and think if a different model specification may produce a better outcome. 

Have a look at the correlation matrix. We see that both `weight` and `length` are correlated with `price`, and therefore we probably want them in our model as controls. However, `weight` and `length` have a positive correlation of 0.9478. These two variables have a very similar behavior. Maybe we do not need both in the model since we may be duplicating the information (a problem will discuss later as *multicollinearity*). Here are two options then. Run two more regressions, one with `weight` and the other one with `length`. Since both variable move so similarly, maybe we can save a degree of freedom by having only one of those two variables. We have now, **three** models in total.

Looking at the summary statistics and correlation matrix you also wonder about whether reparation since 1978 (`rep78`) should be included in the model. This variable a very low correlation with `price` and what seems to be a low standard deviation. Therefore, to complete the robustness check, we will run other two models, with and without `rep78` for each one of the two above specifications. 


To make it easier to compare all these models, it is customary to put them all in one table next to each other. This is what we have in the output below.

{{< figure library="true" src="econometrics/03_OLS/OLS Example 07.png" >}}

---

## Evaluate the quality of your models

There are a number of issues to pay attention to. Look **first** at how some coefficients significantly change in value, such as `mileage`, `length`, `trunk`, and even the `constant`. Some of them even change their sign. This illustrates the importance of evaluating a regression and thinking about which one makes economic sense in order to get the more accurate coefficient estimation. This variance in the estimated coefficients is also a typical indicator *multicollinearity* in the regressors, which we do not know yet how to assess and deal with.

**Second**, look at the bottom part of the table. You can see the degrees of freedom for each model as well as information about the quality of the model. Consider the $R^2$ information. As expected, the model with more regressors has the higher $R^2$. It also happens to have the higher $\bar{R}^2$. Compare, however, the $\bar{R}^2$ of models 3 and 4. Model 3 has less regressors than model 4, and yet has a higher $\bar{R}^2$.

**Third**, look at $RMSE$. According to this measure, model 1 is also the best choice.

**Fourth**, there is the information criteria measures of $AIC$ and $BIC$. According to these measures, Model 1 is also the best model. But, not by much with respect to Model 2.



