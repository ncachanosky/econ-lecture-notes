---
# Title, summary, and page position.
linktitle: "What is hypothesis testing"
weight: 1

# Page metadata.
title: What is hypothesis testing
type: book  # Do not modify.
---



---

## The structure and components of hypothesis testing

In econometrics, most [hypotheses testing](https://en.wikipedia.org/wiki/Statistical_hypothesis_testing) is a method to estimate the likelihood that a certain value is **different** to a given value. In other words, an hypothesis test typically looks at the likelihood that a given estimation is **different** from an assumed value, rather than testing if a given estimation is **equal** to an assumed value.

A reason for this setting is that it is not possible to prove an hypothesis, but only to reject or falsify with certain probability or likelihood. For instance, we cannot prove that a given $beta$ is equal to zero, we can only show the likelihood that **is not** zero.

An hypothesis test usually has four components:
1. The assumed value (the hypothesis)
2. The estimated value (such as a $\hat{\beta})$
3. The probability distribution of the estimation
4. A decision rule to decide whether or not the hypothesis is rejected

The hypothesis under evaluation is presented the following way. The **null hypothesis** $(H_0)$ is the assumption being tested. The **alternative assumption** $(H_A)$ captures all the alternative values the estimation can have.

It is important how you define the null and alternative hypothesis. The alternative hypothesis represents what you expect to find, but is the null hypothesis what you put under test.

Let $\hat{\phi}$ be the estimation of the unobserved value $\phi$.

**Example 1**

>You think the true value of $\phi$ is positive:
>
>1. $H_0: \phi \leq 0$
>2. $H_A: \phi > 0$
>
>See that the alternative hypothesis captures your *guess*, and the null >plus the alternative hypothesis capture all potential values that $\phi$ >can have. If you reject $H_0$, then there is a likelihood that $H_A$ is >true.
>
>The null and alternative hypothesis will look the opposite if you think >the true value of $\phi$ is negative.

**Example 2**
>
>You think that the true value of $\phi$ is different than zero, but you >don't have any particular insight about its sign.
>
>1. $H_0: \phi = 0$
>2. $H_A: \phi \neq 0$
>
>If you can, with some confidence, reject $H_0$, then it has to be the case that there is a likelihood that the true $\phi$ is different than zero.

We can now put together then general structure that most hypothesis testing follow one way or another.

The **first** component is the distance or deviation between the estimated value and the null hypothesis. Consider example 2. Even if it is the case that $\phi = 0$, it is very likely the estimated value will not be exactly zero.

The first component of an hypothesis test is: $\hat{\phi} - H_0$.

Since any estimation of $\phi$ will not be exactly zero, even if the true value of $\phi$ is zero, we need to decide if the difference between the estimated value and $H_0$ is enough to conclude that is unlikely that the true value of $\phi$ is actually zero.

The **second** component of an hypothesis test is measure of variation of the estimated values. Assume the difference between the estimated value and $H_0$ is 10. This tan can be a small if the standard deviation of $\hat{\phi}$ is 1,000 and it can be big if the standard deviation of $\hat{\phi"}$ is 0.1.

The second component component of an hypothesis test is: $\sigma_{\hat{\phi}}$

This second component is used to scale the difference between $\hat{\phi}$ and $H_0$ to a meaningful measure: $\frac{\hat{\phi} - H_0}{\sigma_{\hat{\phi}}}$

The **third** components (probability distribution of $\hat{\phi}$) is used along the **fourth** component (decision rule). The probability distribution is used to get the likelihood that $\hat{\phi} \neq H_0$. At which value of probability we decide that $H_0$ is rejected is the decision rule. We sill see this in more detail below and in the next two sections (*t*-test and F-test).

---

## Type I and Type II errors

Two things can happen when you do an hypothesis test. You can either get the **right** answer or you can get the **wrong** answer. However, there are two types of errors than can yield to a wrong outcome: [Type I error and Type II error](https://en.wikipedia.org/wiki/Type_I_and_type_II_errors)

* **Type I error** is the rejection of a true null hypothesis (false positive)
* **Type II error** is the failure to reject a false null hypothesis (false negative)

The issue is that it is not possible to minimized both types of errors simultaneously. Reducing the probability of having a Type I error increases the probability of having a Type II error (and the other way around).

It can be of importance which error you want to minimize. Assume a Jury must decide if a person accused of homicide is guilty or innocent. It is unlikely that the Jury will not with 100% certainty whether or not the accused is guilty or innocent. Therefore, the judicial procedure needs to decide if it is going to prioritize the error of (1) sending an innocent person to jail (Type I error: false positive) or (2) letting a guilty person free (Type II error: false negative). Because preference is given to let a guilty person walk over incarcerating an innocent person, a Jury typically must come to an unanimous decision **beyond any reasonable doubt**.

The following table depicts the possible outcomes of a hypothesis test, including Type I and Type II errors.

{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Table_01.png" >}}

The **crossover error rate** (CER) is the the point at which the probability of committing each error type are equal. The lower (higher) CER is, the more (less) accurate the hypothesis test is.

---

## Decision rules in hypothesis testing

### Critical values

The hypothesis test produces a value that is compared with a threshold that serves as the decision rule of whether to accept or reject the null hypothesis. For instance, let the threshold to reject the null that $\phi = 0$ is 10. Then, if the difference (in absolute value) between $\hat{\phi}$ and $\phi$ is more than 10, we reject the null and assume that $\phi \neq 0$. But, if the difference is 10, then according to our decision rule the difference is not enough to conclude, with a degree of confidence, that $\phi =neq 0$.

How is the threshold level decided? In two steps. The **first** one is the desired probability of having a Type I error; this probability is usually denoted as $\alpha$. The **second** one is obtaining the value of the threshold from the probability distribution of the estimation. Use the chosen value of $\alpha$ to get the value that, in the probability distribution of $\hat{\phi}$, would produce a probability of $\alpha$. Let $f(\hat{\phi})$ denote the probability distribution of $\hat{\phi}$ and $\phi_C$ the critical (threshold) value. Then: $f(|\phi|>|\phi_C|) = \alpha$. 

The following figure depicts a typical hypothesis testing. The <span style="color:blue">blue</span> line represents the probability distribution of $\hat{\phi}$ assuming that $H_0$ is true. The <span style="color:red">red</span> denotes the critical values that delimit the rejection and fail to reject ("acceptance") regions of $H_0$. Any $\hat{\phi}$ that falls in between $(-\phi_C, \phi_C)$ means that the difference $\hat{\phi} - H_0$ is not enough to reject $H_0$. Alternatively, any $\hat{\phi}$ that falls outside the range $(-\phi_C, \phi_C)$ means that the difference $\hat{\phi} - H_0$ is large enough to reject $H_0$. You can also see that the specific values of $-\phi_C$ and $\phi_C$ depend on the chosen value of $\alpha$ (the probability of having a Type I error).


{{< figure library="true" src="econometrics/05_Hypothesis_Testing/Fig_01.png" >}}

How is $\alpha$ chosen? The easiest way is to follow already stablished conventions. In economics is typically to use 1%, 5%, and 10%, being 5% the most common. A different route would be to consider in more detail the nature of the problem and distribution of the data. If the cost of a Type I error is large, you may want to use a smaller value of $alpha$ (sending astronauts to the moon, or clearing a new vaccine to the general population).

### p-values

### Confidence intervals