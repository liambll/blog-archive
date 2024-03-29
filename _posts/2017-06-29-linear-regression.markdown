---
layout: post
comments: true
title:  "Linear Regression"
title2:  "Linear Regression"
date:   2017-06-29 15:22:00
permalink: /linear-regression/
mathjax: true
tags: Statistics Machine-Learning Linear-Regression Supervised-Learning
categories: Statistics Machine-Learning
img: /blog/assets/linear-regression/linear-regression.png
summary: Linear regression is an approach for modeling the relationship between a scalar dependent variable y and one or more explanatory variables (or independent variables) denoted X...
---


"Linear regression is an approach for modeling the relationship between a dependent variable and one or more explanatory variables."  Linear regression can be used to quantify the strength of relationship between explanatory variables and the dependent variable. It can also be used to predict value of dependent variable based on explanatory variables.
From statistical perspectice, linear regression focuses on the conditional probability distribution of y given X, rather than on the joint probability distribution of y and X, which is the domain of multivariate analysis.

Some examples:
- analyze relationship between customer's satisfaction and customer's waiting time, call duration, discussion topic, etc
- predict house price based on the house's characteristics (location, areas, number of bed rooms, number of bath rooms, etc)

## 1. Description
Relationship between a dependent variable \\(y\\) and k explanatory variables \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\):
\\[
y = f(\mathbf{x}) + \epsilon = w_0 + w_1 x_1 + w_2 x_2 + ... + w_k x_k + \epsilon 
\\]
* \\(y\\) is dependent variable (or output)
* \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\) is a vector of explainatory variables (or inputs) 
* \\(\mathbf{w} = [w_0, x_1, x_2, ..., x_k] \\) is a vector of coefficients (or parameters, weights), in which \\(w_0\\) is bias term and \\(w_i\\) represents strength of linear relationship between \\(y\\) and \\(x_i\\) in the model. If we increase \\(x_i\\) by 1, we would expect \\(y\\) to change by \\(w_i\\).
* \\(\epsilon\\) is error term (or noise) which captures all other factors which influence the dependent variable \\(y\\) other than \\(f(\mathbf{x}) = \mathbf{\bar{x}}\mathbf{w}\\)
<div class="imgcap">
<div >
    <img src="/blog/assets/linear-regression/linear-regression.png" width = "500">
</div>
</div>

__Assumptions__

In statistics, strict linear regression model makes several assumptions about the dependent variables, the explanatory variables and their relationship:
* __Linearity:__ The expected value of the dependent variable is a linear combination of the parameters and the explantory variables. Residual plot is commonly used to visualize any non-linearity relationship.
* __Independence:__ The error term is independent across observations and independent of explantory variables. That means there is little or no multicollinearity among explanatory variables, and there is no auto-correltion among observations. Correlation matrix, Variance Inflation Factor (VIF), Durbin-Watson test are useful to check if indenpendence assumption is violated.
  * Correlation matrix shows correlation between every every variable pair. As a rule of thumb, correlation with absolute value of 0.7-1 indicate strong correlation, 0.4-0.7 indicate moderate correlation, 0-0.4 indicate little correlation.
\\[
corr(X,Y) = \frac{cov(X,Y)}{\sigma_X \sigma_Y}
\\]
  * Variance Inflation Factor (VIF) can be used to measure how much an explanatory variable \\(X_i\\) is depedent on other explanatory variables by formulating the relationship as a regression model. Let's say \\(R_i^2\\) is the coefficient of determination (i.e. the proportion of the variance in the dependent variable that is predictable from the independent variables) in such regression model. VIF for a variable \\(X_i\\) can be caculated as below. VIF > 10 indicates strong multicollinearity.
\\[
VIF_i = \frac{1}{1 - R_i^2}
\\]  
  * Durbin-Watson test is used to detect the presence of autocorrelation (a relationship between values separated from each other by a given time lag) in the residuals. If \\(e_t\\) is the residual associated with observation at time \\(t\\), Durbin-Watson statistics can be caculated as below. As a rule of thumb, Durbin-Watson statistics smaller than 1 or greater than 3 indicates significant positive/negative autocorrelation.
\\[
d = \frac{\sum_{t=2}^T (e_t - e_{t-1})^2}{\sum_{t=1}^T e_t^2}
\\]   
* __Homoscedasticity:__ The error between observed and predicted values (i.e. the residuals of the regression) should have constant variance. Goldfeld-Quandt test can be used to detect Heteroskedasticity by dividing a dataset into two subsets in which the observations for which the pre-identified explanatory variable takes the lowest values are in one subset, with higher values in the other. Goldfeld-Quandt test statistic is caculated as the ratio of the mean square residual errors for the regressions on the two subsets. The test corresponds to an [F-test](https://en.wikipedia.org/wiki/F-test_of_equality_of_variances) of equality of variances.
* __Normality:__ The error term should be normally distributed. Kolmogorov–Smirnov (KS) test is used to detect non-normality. Kolmogorov–Smirnov test (KS test) is a test of the equality of two continuous, one-dimensional probability distributions. For testing for normality of a distribution \\(P\\), samples in \\(P\\) are standardized and compared to a referenced standard normal distribution with the same mean and variance as \\(P\\). If _sup_ is the [supremum](https://en.wikipedia.org/wiki/Infimum_and_supremum) of the set of distances, KS statistics is caculated as below.
\\[
D = sup_x \|F_P(x) - F(x)\|
\\] 

If any assumption is severely violated, it needs to be handled by performing variable transformation (non-linear transformation, Box-Cox transformation, etc) before any meaningful conclusion can be drawn based on the model.

## 2. Math
Given a dataset of \\(N\\) observations, we want to find a set of coefficients \\(\mathbf{w}\\) so that the predicted value \\(f(\mathbf{x})\\) can accurately represent observed value \\(y\\) the most.

__Loss function__

In machine learning, we achieve this objective by minimize a lost function representing the difference between the predicted value f(\mathbf{x}) and observed value \\(y\\). There is no defined rule on what is the correct loss function. The most common technique is ordinary least squares in which we try to minimize sum of square errors over all observations:
\\[
E(\mathbf{w}) = \frac{1}{2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]
We can try to minimize the sum of absolute error over all observations, and in this case, we penalize wrong prediction less.
\\[
E(\mathbf{w}) = \sum_{i=1}^N \|y\_i - \mathbf{\bar{x}\_i}\mathbf{w}\|
\\]
We can also minimize a penalized version of the least squares loss function.
\\[
E(\mathbf{w}) = \frac{1}{2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2 + \sum \mathbf{w}^2
\\]
As you can see, machine learning techniques try to formulate problem in terms of minimizing a loss function based on certain intuition, and in doing so, we hope to achieve the best prediction.

In statistics, we approach the problem using a technique call Maximum Likelihood Estimation (MLE): what is the set of coeeficients \\(\mathbf{w}\\) that maximize the likelihood that N observations would happen. Since linear model assume the error term to be normally distributed with constant variance \\(\sigma^2\\), the probability density function of \\(y\\) given \\(\mathbf{x}\\) and \\(\mathbf{w}\\) is:
\\[
P(Y=y_i|X=\mathbf{\bar{x}\_i};\mathbf{w};\sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}}\exp{-\frac{(y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2}{2\sigma^2}}
\\]

The likelihood function for data would be:
\\[
\mathcal{L}(\mathbf{w}) = \prod_{i=1}^N \frac{1}{\sqrt{2\pi\sigma^2}}\exp{-\frac{(y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2}{2\sigma^2}}
\\]
Maximizing likelihood is equipvalent to minimizing negative log-likelihood:
\\[
\-log~\mathcal{L}(\mathbf{w}) = \frac{N}{2}log{2\pi} + Nlog{\sigma} + \frac{1}{2\sigma^2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]
Therefore, maximizing likelihood ends up being equivalent to minimizing sum of square errors over all observations.

__Parameter Estimates__

We estimate coefficients by taking first-order deriative of the log-likelihood:
\\[
\frac{\partial log~\mathcal{L}(\mathbf{w})}{\partial \mathbf{w}} = 0
\\]
It has a closed form solution:
\\[
\mathbf{w} = (\mathbf{\bar{X}}^T\mathbf{\bar{X}})^{-1} \mathbf{\bar{X}}^T\mathbf{y}
\\]
in which:
* \\(\mathbf{y} = [y_1; y_2; \dots; y_N]\\)
* \\(\mathbf{\bar{X}} = [\mathbf{\bar{x}}_1; \mathbf{\bar{x}}_2; \dots; \mathbf{\bar{x}}_N ] \\)

However, we usually use gradient descent to approximate \\(\mathbf{w}\\) instead to avoid large matrix computation.

__Variance matrix estimates__

In machine learning, estimated \\(\mathbf{w}\\) is all we need in order to perform prediction. In statistics, we usually want to get the variance matrix for coefficients in order to caculate confidence intervals at a specific significant level for coefficients and prediction. For that, we need to obtain Hessian matrix by taking second-order derivative of the log-likelihood:
\\[
\frac{\partial^2 log~\mathcal{L}(\mathbf{w})}{\partial^2 \mathbf{w}} = 0
\\]
The estimated variance matrix is the inverse of Hessian matrix.
