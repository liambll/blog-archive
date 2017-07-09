---
layout: post
comments: true
title:  "Hypothesis Testing"
title2:  "Hypothesis Testing"
date:   2017-07-09 15:22:00
permalink: /hypothesis-testing/
mathjax: true
tags: Statistics Hypothesis-Testing
categories: Statistics
img: /blog/assets/hypothesis-testing/hypothesis-testing.png
summary: Hypothesis testing is a confirmatory data analysis procedure to confirm or reject a statistical hypothesis...
---


Hypothesis testing is a confirmatory data analysis procedure to confirm or reject a statistical hypothesis. The general procedure for hypothesis testing involves 3 steps:
* Make an initial assumption
* Collect sample data
* Decide whether to reject or not reject the initial assumption, based on the sample data

## 1. Description
In hypothesis testing, we first define two hypothesis:
* __Null hypothesis \\(H_0\\):__ an assumption that we want to reject
* __Alternative hypothesis \\(H_a\\):__ a "rivalry" assumption that is contrary to the null hypothesis

We always assume the null hypothesis is true and then collect evidence (sample data) to draw conclusion about that assumption __at a certain level of confidence__. Please note that we can never be 100% confidence and accept a hypothesis. Therefore, we usually say __reject__ or __fail to reject__ a hypothesis. There are two types of error in hypothesis testing:
<div class="imgcap">
<div >
    <img src="/blog/assets/hypothesis-testing/error-type.png" width = "600">
</div>
</div>

* __Type I error:__ also known as false positive, happens when we reject the null hypothesis when in fact it is true. The type I error rate or __significance level \\(\alpha\\)__ is the probability of rejecting the null hypothesis given that it is true. __Confidence level__ is the probability of correctly not rejecting the null hypothesis given that it is true.
\\[
Confidence ~level = 1 - \alpha
\\]
The significance level is usually set to 0.05 (5%), implying that there is 5% probability of incorrectly rejecting the null hypothesis.

* __Type II error:__ also known as false negative, happens when we fail to reject the null hypothesis when in fact it is false. The type II error rate or __\\(\beta\\)__ is the probability of incorrectly rejecting the null hypothesis given that it is false. __Power of test__ is the probability of correctly rejecting the null hypothesis given that it is false.
\\[
Power ~of ~test = 1 - \beta
\\]
If the sample size is fixed, decreasing Type I error rate \\(\alpha\\) will increase Type II error rate \\(\beta\\). If we want both error rates to decrease, we need to increase the sample size.
<div class="imgcap">
<div >
    <img src="/blog/assets/hypothesis-testing/power.jpg" width = "500">
</div>
</div>

__P-value__

After observing data (by collecting evidence), we can calculate certain test statistics __T__. P-value is the probability, given the null hypothesis, of having the test statistic __T__ at least as extreme in the direction of the alternative hypothesis as what was observed.
* If the P-value is small, say less than or equal to \\(\alpha\\), it is "unlikely" that we would observe the test statistic __T__ at least as extreme in the direction of the alternative hypothesis. Therefore, we reject the null hypothesis.
* If the P-value is large, say more than \\(\alpha\\), it is "likely" that we would observe the test statistic __T__ at least as extreme in the direction of the alternative hypothesis. Therefore, we fail to reject the null hypotehsis.


## 2. Common Hypothesis tests
Many test statistics are caculated based on its normal distribution approximation for large samples ([central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem)). It should be emphasized that when sample size is small (eg. due to limited data available), such approximation is no longer appropriate and [extact test](https://en.wikipedia.org/wiki/Exact_test) should be used. Below are common tests:

__Test of equality of two means__


__Test of equality of two variances__


__Test of association__


## 3. Simpson's Paradox
While making statistical inference using hypothesis testing, we should be aware of Simpson's paradox, which is a phenomenon in which a trend appears in different groups of data but disappears or reverses when these groups are combined. Simpson's paradox is usually caused by a [confounder](https://en.wikipedia.org/wiki/Confounding), i.e. a variable that has strong influence on other variables in the hypothesis test.
