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
P(y=1|\mathbf{x}; \mathbf{w}) = sigmoid(\mathbf{w}^T\mathbf{x})
\\]

* asdas \\(P(y=1|\mathbf{x}; \mathbf{w})\\)
* sigmoid is called an activation function. Output of sigmoid function is always between 0 and 1:
\\[
sigmoid(t) = \frac{1}{1 + e^{-t}}
\\]
* \\(\mathbf{w}^T\mathbf{x}\\) is linear combination of explanatory variables \\([x_1, x_2, ..., x_k] \\)
* \\(\mathbf{w} = [w_0, x_1, x_2, ..., x_k] \\) is a vector of coefficients (or parameters, weights), in which \\(w_0\\) is bias term and \\(w_i\\) represents strength of linear relationship between log odd, i.e. the probability of \\(y\\) being 1 vs the probability of \\(y\\) being 0, and \\(x_i\\) in the model
\\[
log~frac{P(y\_i = 1 | \mathbf{x}\_i; \mathbf{w})}{1 - P(y\_i = 1 | \mathbf{x}\_i; \mathbf{w})} = \mathbf{w}^T\mathbf{x}
\\]
