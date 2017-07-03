---
layout: post
comments: true
title:  "Logistic Regression"
title2:  "Logistic Regression"
date:   2017-06-30 10:22:00
permalink: /logistic-regression/
mathjax: true
tags: Statistics Machine-Learning Logistic-Regression Supervised-Learning
categories: Statistics Machine-Learning
img: /blog/assets/logistic-regression/logistic-regression.png
summary: Logistic regression is a regression model where the dependent variable is binary...
---


"Logistic regression is a regression model where the dependent variable is binary (0 or 1)."
Some examples:
* analyze association between mortality rate and smoking habit
* predict whether borrowers would default based on historical product holdings and account balances.

## 1. Model
Relationship between the probability of \\(y\\) being 1 and and k explanatory variables \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\):
\\[
P(y=1\|\mathbf{x}; \mathbf{w}) = f(\mathbf{w}^T\mathbf{x})
\\]

* \\(P(y=1\|\mathbf{x}; \mathbf{w})\\) is the probability of \\(y\\) being 1. The probability of \\(y\\) being 0 would then be 1 - \\(P(y=1\|\mathbf{x}; \mathbf{w})\\).
* \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\) is a vector of explainatory variables
* Link function \\(f\\) is logistic sigmoid in this case. Sigmoid function has S -shape with output always between 0 and 1:
\\[
sigmoid(t) = \frac{1}{1 + e^{-t}}
\\]
* \\(\mathbf{w} = [w_0, x_1, x_2, ..., x_k] \\) is a vector of coefficients (or parameters, weights), in which \\(w_0\\) is bias term and \\(w_i\\) represents strength of linear relationship between log odd, i.e. the probability of \\(y\\) being 1 vs the probability of \\(y\\) being 0, and \\(x_i\\) in the model. If we increase \\(x_i\\) by 1, we would expect the odd of \\(y\\) being 1 vs being 0 to change by \\(exp(w_i)\\).
\\[
log~\frac{P(y = 1 \| \mathbf{x}; \mathbf{w})}{1 - P(y = 1 \| \mathbf{x}; \mathbf{w})} = \mathbf{w}^T\mathbf{x}
\\]

__Assumptions__
In statistics, logistic regression model makes several assumptions such as linearity between log odd and explanatory variables, error term being independent across observations and independent of explantory variables.

## 2. Estimation
Given a dataset of \\(N\\) observations, we want to find a set of coefficients \\(\mathbf{w}\\) so that the predicted value \\(f(sigmoid(\mathbf{x}))\\) can accurately represent observed value \\(P(y=1\|\mathbf{x}; \mathbf{w})\\) the most.

Since \\(y\\) follows Bernoulli distribution (i.e. 0 or 1), the probability density function of \\(y\\) given \\(\mathbf{x}\\) and \\(\mathbf{w}\\) is:
\\[
P(Y=y\_i| \ X = \mathbf{x}\_i; \mathbf{w}) = f(\mathbf{w}^T\mathbf{x}\_i)^{y_i}\(1 - f(\mathbf{w}^T\mathbf{x}\_i))^{1- y_i}
\\]
The likelihood function for data would be:
\\[
\mathcal{L}(\mathbf{w}) = \prod_{i=1}^N f(\mathbf{w}^T\mathbf{x}\_i)^{y_i}\(1 - f(\mathbf{w}^T\mathbf{x}\_i))^{1- y_i}
\\]
Maximizing likelihood is equipvalent to minimizing negative log-likelihood:
\\[
\-log~\mathcal{L}(\mathbf{w}) = = -\sum\_{i=1}^N(y\_i \log f(\mathbf{w}^T\mathbf{x}\_i) + (1-y\_i) \log (1 - f(\mathbf{w}^T\mathbf{x}\_i)))
\\]
On a side note, negative log-likelihood in this case is the same cross-entropy loss, which measures the diffences between two probability distribution. Therefore, we can also think of the problem as minimizing the difference between true probability distribution \\(y\\) and estimated probability distribution \\(f(\mathbf{w}^T\mathbf{x})\\).

There is no closed form solution for logistic regression due to the presence of link function \\(f\\). We can use gradient descent to estimate coefficients and then calculate variance matrix for coefficients.


## 3. Multi-class classification
We can extend logistic regression model to handle cases when the dependent variable is categorical with more than 2 values, i.e. multi-nomial distribution. Several common extensions are:
- __One vs All model:__ Build C logistic regression models, each predicting odd of \\(y\\) being class \\(C\_i\\) vs not being class \\(C\_i\\). Then, choose class with the highest probability out of C predictions.
\\[
log~\frac{P(y = C\_i \| \mathbf{x}; \mathbf{w}\_i)}{1 - P(y = C\_i \| \mathbf{x}; \mathbf{w}\_i)} = \mathbf{w\_i}^T\mathbf{x}
\\]
- __One vs One model:__ Build C(C-1)/2 logistics regression models, each predicting odd of \\(y\\) being class \\(C\_i\\) vs being class \\(C\_j\\). Then, choose class with the most votes out of C(C-1)/2 predictions.
\\[
log~\frac{P(y = C\_i \| \mathbf{x}; \mathbf{w}\_{ij})}{P(y = C\_j \| \mathbf{x}; \mathbf{w}\_{ij})} = \mathbf{w\_{ij}}^T\mathbf{x}
\\]
- __Baseline category logit model:__ similar to One vs All approach. Build (C-1) logistic regression models, each predicting odd of \\(y\\) being class \\(C\_i\\) vs being class \\(C\_1\\). Then, calculate probability for C classes and choose class with the highest probability.
\\[
log~\frac{P(y = C\_i \| \mathbf{x}; \mathbf{w}\_i)}{P(y = C\_1 \| \mathbf{x}; \mathbf{w}\_ij)} = \mathbf{w\_i}^T\mathbf{x}
\\]
- __Cumulative logit model:__ usually apply for ordinal categorical dependent variable. Build (C-1) logistic regression models, each predicting odd of \\(y\\) being not greater than \\(C\_i\\) vs being greater \\(C\_i\\). Then, calculate probability for C classes and choose class with the highest probability.
\\[
log~\frac{P(y \leq C\_i \| \mathbf{x}; \mathbf{w}\_i)}{P(y > C\_i \| \mathbf{x}; \mathbf{w}\_i)} = \mathbf{w\_i}^T\mathbf{x}
\\]
- __Adjacent category logit model:__ usually apply for ordinal categorical dependent variable. Build (C-1) logistic regression models, each predicting odd of \\(y\\) being class \\(C\_{i+1}\\) vs being class \\(C\_i\\). Then, calculate probability for C classes and choose class with the highest probability.
\\[
log~\frac{P(y = C\_{i+1} \| \mathbf{x}; \mathbf{w}\_i)}{P(y = C\_i \| \mathbf{x}; \mathbf{w}\_i)} = \mathbf{w\_i}^T\mathbf{x}
\\]

Multi-class classification can also be handled using __Softmax regression model__ which is a __Neural Network__ model.
