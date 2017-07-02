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

## 1. Model
Relationship between a dependent variable \\(y\\) and k explanatory variables \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\):
\\[
y = f(\mathbf{x}) + \epsilon = w_0 + w_1 x_1 + w_2 x_2 + ... + w_k x_k + \epsilon 
\\]
* \\(y\\) is dependent variable (or output)
* \\(\mathbf{x} = [x_1, x_2, ..., x_k] \\) is a vector of explainatory variables (or inputs) 
* \\(\mathbf{w} = [w_0, x_1, x_2, ..., x_k] \\) is a vector of coefficients (or parameters, weights), in which \\(w_0\\) is bias term and \\(w_i\\) represents strength of linear relationship between y and \\(x_i\\) in the model
* \\(\epsilon\\) is error term (or noise) which captures all other factors which influence the dependent variable \\(y\\) other than \\(f(\mathbf{x}) = \mathbf{\bar{x}}\mathbf{w}\\)

__Assumptions__

In statistics, strict linear regression model makes several assumptions about the dependent variables, the explanatory variables and their relationship:
* Linearity: The expected value of the dependent variable is a linear combination of the parameters and the explantory variables.
* Independence: The error term is independent across observations and independent of explantory variables. That means there is little or no multicollinearity among explanatory variables, and there is no auto-correltion among observations.
* Homoscedasticity: The error between observed and predicted values (i.e. the residuals of the regression) should have constant variance.
* Normality: The error term should be normally distributed

## 2. Estimation
Given a dataset of \\(N\\) observations, we want to find a set of coefficients \\(\mathbf{w}\\) so that the predicted value \\(f(\mathbf{x})\\) can accurately represent observed value \\(y\\) the most.

__Machine Learning__

We achieve this objective by minimize a lost function representing the difference between the predicted value f(\mathbf{x}) and observed value \\(y\\). There is no defined rule on what is the correct loss function. The most common technique is ordinary least squares in which we try to minimize sum of square errors over all observations:
\\[
\mathcal{L}(\mathbf{w}) = \frac{1}{2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]
We can try to minimize the sum of absolute error over all observations, and in this case, we penalize wrong prediction less. We can slo minimize a penalized version of the least squares loss function. As you can see, machine learning techniques try to formulate problem in terms of minimizing a loss function based on certain intuition, and in doing so, we hope to achieve the best prediction.

__Statistics__
We approach the problem using a technique call Maximum Likelihood Estimation (MLE): what is the set of coeeficients \\(\mathbf{w}\\) that maximize the likelihood that N observations would happen. Since linear model assume the error term to be normally distributed with constant variance \\(\sigma^2\\), the probability density function of \\(y\\) given \\(\mathbf{x}\\) and \\(\mathbf{w}\\) is:
\\[
p(y_i|\mathbf{x}=x_i;\mathbf{w};\sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}}\exp{-\frac{(y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2}{2\sigma^2}}
\\]

The likelihood function for data would be:
\\[
\mathcal{l}(\mathbf{w}) = \prod_{i=1}^N \frac{1}{\sqrt{2\pi\sigma^2}}\exp{-\frac{(y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2}{2\sigma^2}}
\\]
Maximizing likelihood is equipvalent to minimizing negative log-likelihood:
\\[
\-log~\mathcal{l}(\mathbf{w}) = \frac{N}{2}log{2\pi} + Nlog{\sigma} + \frac{1}{2\sigma^2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]
Therefore, maximizing likelihood ends up being equivalent to minimizing sum of square errors over all observations.

Using derivatives, minimizing sum of square errors over all observations has a closed form solution:
\\[
\mathbf{w} = (\mathbf{\bar{X}}^T\mathbf{\bar{X}})^{\dagger} \mathbf{\bar{X}}^T\mathbf{y}
\\]
in which:
* \\(\mathbf{y} = [y_1; y_2; \dots; y_N]\\)
* \\(\mathbf{\bar{X}} = [\mathbf{\bar{x}}_1; \mathbf{\bar{x}}_2; \dots; \mathbf{\bar{x}}_N ] \\)
To avoid huge matrix computation, we can use gradient descent to approximate \\(w\\) instead. I will not go into details on these topics here.
