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
    <img src="/blog/assets/hypothesis-testing/error-type.png" width = "400">
</div>
</div>
* __Type I error:__ also known as false positive, happens when we reject the null hypothesis when in fact it is true. The type I error rate or __significance level \\(\alpha\\)__ is the probability of rejecting the null hypothesis given that it is true. __Confidence level__ is the probability of correctly not rejecting the null hypothesis given that it is true.
\\[
Confidence ~level = 1 - \alpha
\\]
The significance level is usually to 0.05 (5%), implying that there is 5% probability of incorrectly rejecting the null hypothesis.
* __Type II error:__ also known as false negative, happens when we fail to reject the null hypothesis when in fact it is false. The type II error rate or __\\(\beta\\)__ is the probability of incorrectly rejecting the null hypothesis given that it is false. __Power of test__ is the probability of correctly rejecting the null hypothesis given that it is false.
\\[
Power ~of ~test = 1 - \beta
\\]

* Sample size
* Significant Level
* p-value
* Power of test


## 2. Common Hypothesis test



## 3. Hypothesis testing with small smaple size
