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

Let us use the *auto* dataset in `STATA` and assume we want to study the price of cars $(y)$ as a function of mileage (mpg) $(x)$.

Consider first **how** is your data stored. If you are working with `STATA`, or any other statistical package, you may be lucky and have access to the data in your software format. All you need to is load the file to your software. For instance, STATA data files have the `.dta` extension.

However, it is possible that data stored in a more general format, just as `.csv` or Excel file. It is also possible that you will have to build your dataset before *importing* into your statistical software.

Unless the data you need is already in a dataset (of one format or another, you will have to create your own dataset. If that is the case, you may want to consider *how* you order your data.

Let us use an hypothetical example (unrelated to the automobile exercise) to show how you can organize your dataset to make it easy to read and explore. Assume you are looking at data for the 50 U.S. states.

Data is usually organized the following way. Regressors are columns and rows are observations. In addition, you know you have three types of variables: (1) the **dependent** variable, (2) your regressors **of interest**, (3) and our **control** variables. Then, you can start with some metadata such as the observation number and the U.S. state. Each row is one observation (or one state). This metadata helps to identify each row. Then you can identify (with borders or different colors) your dependent variable. To the right you can have your variable(s) of interest. Finally, the last set of columns can be your control variables. You may also want to consider other *format* edits that will facilitate your reading of the data such as number of decimals, or horizontal lines every a few observations, and so on).

The figure below is an example of how a user-friendly dataset in Excel may look like.

{{< figure library="true" src="econometrics/03_OLS/Fig_09.png" >}}

{{<icon name="file-excel" pack="fas" >}} {{% staticref "media/econometrics/03_OLS/Dataset format example.xlsx" %}}Download Excel sample file.{{% /staticref %}}

A user-friendly format of your dataset is important because you may need to some data exploration at some point in your regression exercise. The easier it is to look at the screen when you need to identify particular observations, the easier and quicker you can find what you are looking for.

---

## Familiarize your self with the data

### Statistical summary

### Correlation matrices

### Scatter plots

---

## Define your models

---

## Run your regressions

---

## Evaluate the quality of your models