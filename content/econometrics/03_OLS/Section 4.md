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


---

## Define your models

---

## Run your regressions

---

## Evaluate the quality of your models