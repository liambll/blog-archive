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


## 2. Math
Many test statistics are caculated based on asymptotically normal distribution approximation for large samples ([central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem)). Let's assume we perform a Hypothesis test with large sample size = \\(N\\) at significant level \\(\alpha\\) and the test statistics has asymptotically normal distribution with variance \\(\sigma^2\\).
\\[
H_0: \mu = \mu_0
H_a: \mu > \mu_0
\\]



Below are common test statistics:
* __One sample z-test:__ test population mean when population variance is known
\\[
z = \frac{\bar{x}-\mu_0}{ \frac{\sigma} {\sqrt{n}}}
\\]

* __Two sample z-test:__ test difference between two population means when population variances are known
\\[
z = \frac{(\bar{x_1} - \bar{x_2}) - d_0}{\sqrt{ \frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}}
\\]

* __One sample t-test:__ test population mean when population variance is unknown
\\[
t = \frac{\bar{x}-\mu_0}{ \frac{s}{\sqrt{n}}} \\\
df = n - 1
\\]

* __Two sample pooled t-test:__ test difference between two population means when population variances are equal but unknown
\\[
t = \frac{(\bar{x_1} - \bar{x_2}) - d_0}{s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}} \\\
s_p^2 = \frac{ (n_1-1)s_1^2 + (n_2-1)s_2^2 }{ n_1 + n_2 - 2 } \\\
df = n_1 + n_2 - 2
\\]

* __Two sample unpooled t-test:__ test difference between two population means when population variances are unequal and unknown
\\[
t = \frac{(\bar{x_1} - \bar{x_2}) - d_0}{\sqrt{ \frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}} \\\
df = \frac{ (\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2})^2 }{ \frac{(\frac{s_1^2}{n_1})^2}{n_1-1} + \frac{(\frac{s_2^2}{n_2})^2}{(n_2-1)}  }
\\]

* __Paired t-test:__ test difference between two population means on the same subjects (eg. before and after)
\\[
t = \frac{\bar{d} - d_0}{\frac{s_d}{\sqrt{n}} } \\\
df = n - 1
\\]

* __One proportion z-test:__ test population proportion
\\[
z = \frac{ \hat{p} - p_0 }{ \sqrt{\frac{p_0(1-p_0)}{n}} }
\\]

* __Two proportion pooled z-test:__ test if two population proportions are equal
\\[
z = \frac{ \hat{p_1} - \hat{p_2} }{ \sqrt{ \hat{p}(1-\hat{p})(\frac{1}{n_1} + \frac{1}{n_2}) } } \\\
\hat{p} = \frac{x_1 + x_2}{n_1 + n_2}
\\]

* __Two proportion unpooled z-test:__ test difference between two population proportions
\\[
z = \frac{ (\hat{p_1} - \hat{p_2}) - d_0 }{ \sqrt{ \frac{\hat{p_1}(1-\hat{p_1})}{n_1} + \frac{\hat{p_2}(1-\hat{p_2})}{n_2} } }
\\]

* __F-test:__ test equality of two population variances
\\[
F = \frac{s_1^2}{s_2^2} \\\
s_1^2 > s_2^2 \\\
df_1 = n_1 - 1, ~df_2 = n_2 - 1
\\]

* __Chi-square test:__ test association between two population
\\[
\chi^2 = \sum^k \frac{(observed - expected)^2}{expected} \\\
df = k - 1
\\]

It should be emphasized that when sample size is small (eg. due to limited data available), such approximation is no longer appropriate and [extact test](https://en.wikipedia.org/wiki/Exact_test) should be used. 

## 3. Simpson's Paradox
While making statistical inference using hypothesis testing, we should be aware of Simpson's paradox, which is a phenomenon in which a trend appears in different groups of data but disappears or reverses when these groups are combined. Simpson's paradox is usually caused by a [confounder](https://en.wikipedia.org/wiki/Confounding), i.e. a variable that has strong influence on other variables in the hypothesis test.
